# Блокировки

## Настройте сервер так, чтобы в журнал сообщений сбрасывалась информация о блокировках, удерживаемых более 200 миллисекунд. Воспроизведите ситуацию, при которой в журнале появятся такие сообщения.

```
postgres=# ALTER SYSTEM SET log_lock_waits = on;
ALTER SYSTEM
postgres=# SELECT pg_reload_conf();
 pg_reload_conf
----------------
 t
(1 row)
postgres=#
```

```
postgres=# ALTER SYSTEM SET deadlock_timeout = 200;
ALTER SYSTEM
postgres=# SELECT pg_reload_conf();
 pg_reload_conf
----------------
 t
(1 row)

postgres=# SHOW deadlock_timeout;
 deadlock_timeout
------------------
 200ms
```

```
postgres=# create table dl (dead1 int);
CREATE TABLE
postgres=# insert into locks values (1), (2);
INSERT 0 2
postgres=# select * from dl;
 1 
 2

postgres=# begin;
BEGIN
postgres=*# update dl set dead1 = 5 where dead = 1;
UPDATE 1
postgres=#
```

Вторая сессия 

```
postgres=# update dl set dead1 = 7 where dead = 1;
```

Первая сессия

```
postgres=*# commit;
COMMIT
postgres=#
```

Вторая сессия сразу же отработала 

```
postgres=# update dl set dead = 7 where dead = 1;
UPDATE 1
postgres=#
```

Результат работы в журнале

```
2022-08-16 11:10:42.047 UTC [1603] postgres@postgres LOG:  process 1603 still waiting for ShareLock on transaction 2829554 after 200.010 ms
2022-08-16 11:10:42.047 UTC [1603] postgres@postgres DETAIL:  Process holding the lock: 1205. Wait queue: 1603.
2022-08-16 11:10:42.047 UTC [1603] postgres@postgres CONTEXT:  while updating tuple (0,3) in relation "dl"
2022-08-16 11:10:42.047 UTC [1603] postgres@postgres STATEMENT:  update dl set dead = 7 where dead = 1;
2022-08-16 11:10:51.411 UTC [1603] postgres@postgres LOG:  process 1603 acquired ShareLock on transaction 2829554 after 8674.101 ms
2022-08-16 11:10:51.411 UTC [1603] postgres@postgres CONTEXT:  while updating tuple (0,3) in relation "locks"
```

## Смоделируйте ситуацию обновления одной и той же строки тремя командами UPDATE в разных сеансах. Изучите возникшие блокировки в представлении pg_locks и убедитесь, что все они понятны. Пришлите список блокировок и объясните, что значит каждая.

```
CREATE VIEW locks_v AS
SELECT pid,
       locktype,
       CASE locktype
         WHEN 'relation' THEN relation::regclass::text
         WHEN 'transactionid' THEN transactionid::text
         WHEN 'tuple' THEN relation::regclass::text||':'||tuple::text
       END AS lockid,
       mode,
       granted
FROM pg_locks
WHERE locktype in ('relation','transactionid','tuple')
AND (locktype != 'relation' OR relation = 'accounts'::regclass or relation = 'accounts_pkey'::regclass);
```

Выполнили Update, получили результат: 

```
postgres=# select * from locks_v;
 pid  |   locktype    |    lockid     |       mode       | granted
------+---------------+---------------+------------------+---------
 1230 | relation      | accounts_pkey | RowExclusiveLock | t
 1230 | relation      | accounts      | RowExclusiveLock | t
 1541 | relation      | accounts_pkey | RowExclusiveLock | t
 1541 | relation      | accounts      | RowExclusiveLock | t
 1485 | relation      | accounts_pkey | RowExclusiveLock | t
 1485 | relation      | accounts      | RowExclusiveLock | t
 1485 | transactionid | 7329573       | ExclusiveLock    | t
 1230 | tuple         | accounts:1    | ExclusiveLock    | f
 1541 | transactionid | 7329574       | ExclusiveLock    | t
 1541 | tuple         | accounts:1    | ExclusiveLock    | t
 1230 | transactionid | 7329575       | ExclusiveLock    | t
 1541 | transactionid | 7329573       | ShareLock        | f
(12 rows)
```

В результате есть 3 транзакции в своих процессах. По наблюдениям, заблокированы таблица и первичный ключ. Процессы 1230 и 1541 заблокированы в ожидании. 

## Воспроизведите взаимоблокировку трех транзакций. Можно ли разобраться в ситуации постфактум, изучая журнал сообщений?

```
2022-08-16 11:22:31.839 UTC [1124] postgres@postgres LOG:  process 1124 still waiting for ShareLock on transaction 7429577 after 200.001 ms
2022-08-16 11:22:31.839 UTC [1124] postgres@postgres DETAIL:  Process holding the lock: 1532. Wait queue: 1124.
2022-08-16 11:22:31.839 UTC [1124] postgres@postgres CONTEXT:  while updating tuple (0,3) in relation "accounts"
2022-08-16 11:22:31.839 UTC [1124] postgres@postgres STATEMENT:  update accounts set amount = amount + 1 where acc_no = 32;
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres LOG:  process 1532 detected deadlock while waiting for ShareLock on transaction 7429576 after 200.150 ms
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres DETAIL:  Process holding the lock: 1124. Wait queue: .
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres CONTEXT:  while updating tuple (0,2) in relation "accounts"
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres STATEMENT:  update accounts set amount = amount + 5 where acc_no = 20;
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres ERROR:  deadlock detected
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres DETAIL:  Process 1532 waits for ShareLock on transaction 7429576; blocked by process 1124.
        Process 1124 waits for ShareLock on transaction 7429577; blocked by process 1532.
        Process 1532: update accounts set amount = amount + 5 where acc_no = 20;
        Process 1124: update accounts set amount = amount + 1 where acc_no = 32;
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres HINT:  See server log for query details.
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres CONTEXT:  while updating tuple (0,2) in relation "accounts"
2022-08-16 11:22:48.253 UTC [1532] postgres@postgres STATEMENT:  update accounts set amount = amount + 5 where acc_no = 20;
2022-08-16 11:22:48.253 UTC [1124] postgres@postgres LOG:  process 1124 acquired ShareLock on transaction 7429577 after 16614.096 ms
2022-08-16 11:22:48.253 UTC [1124] postgres@postgres CONTEXT:  while updating tuple (0,3) in relation "accounts"
2022-08-16 11:22:48.253 UTC [1124] postgres@postgres STATEMENT:  update accounts set amount = amount + 1 where acc_no = 32;
```

Учитывая что в предыдущем задании был разбор блокировок с участием 3 транзакций, без использования журнала, и имея предсказуемое поведение, понятно что даже в двух транзакциях можно будет разобраться в журнале. 
В случае с рабочим проектом, где происходят множественные блокировки, сложность разбора по журналу или при помощи встроенных блокировок будет возрастать прямо пропорционально количеству данных блокировок, что косвенно приведет к продолжительному поиску источника.


## Могут ли две транзакции, выполняющие единственную команду UPDATE одной и той же таблицы (без where), заблокировать друг друга? 

В теории это возможно.