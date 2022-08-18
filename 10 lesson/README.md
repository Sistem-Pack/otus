# Журналы

## Настройте выполнение контрольной точки раз в 30 секунд.

```
root@user-virtual-machine:~# echo "checkpoint_timeout = 30s" | sudo tee -a /etc/postgresql/14/main/postgresql.conf
checkpoint_timeout = 30s
root@user-virtual-machine:~# sudo systemctl restart postgresql
root@user-virtual-machine:~#
```

## 10 минут c помощью утилиты pgbench подавайте нагрузку.

root@user-virtual-machine:~# echo "checkpoint_timeout = 30s" | sudo tee -a /etc/postgresql/14/main/postgresql.conf
checkpoint_timeout = 30s
root@user-virtual-machine:~# sudo systemctl restart postgresql
root@user-virtual-machine:~# sudo -u postgres psql -c "select pg_stat_reset()"
could not change directory to "/root": Отказано в доступе
 pg_stat_reset
---------------

(1 row)

root@user-virtual-machine:~# sudo -u postgres psql -c "select pg_stat_reset_shared('bgwriter')"
could not change directory to "/root": Отказано в доступе
 pg_stat_reset_shared
----------------------

(1 row)

root@user-virtual-machine:~# sudo du -h /var/lib/postgresql/14/main/pg_wal # 17mb
4,0K    /var/lib/postgresql/14/main/pg_wal/archive_status
17M     /var/lib/postgresql/14/main/pg_wal
root@user-virtual-machine:~# sudo -u postgres pgbench -i postgres
dropping old tables...
ЗАМЕЧАНИЕ:  таблица "pgbench_accounts" не существует, пропускается
ЗАМЕЧАНИЕ:  таблица "pgbench_branches" не существует, пропускается
ЗАМЕЧАНИЕ:  таблица "pgbench_history" не существует, пропускается
ЗАМЕЧАНИЕ:  таблица "pgbench_tellers" не существует, пропускается
creating tables...
generating data (client-side)...
100000 of 100000 tuples (100%) done (elapsed 0.06 s, remaining 0.00 s)
vacuuming...
creating primary keys...
done in 0.17 s (drop tables 0.00 s, create tables 0.00 s, client-side generate 0.09 s, vacuum 0.05 s, primary keys 0.03 s).
root@user-virtual-machine:~# sudo -u postgres pgbench -c8 -P 60 -T 600 -U postgres postgres
pgbench (14.5 (Ubuntu 14.5-1.pgdg20.04+1))
starting vacuum...end.
progress: 60.0 s, 2169.9 tps, lat 3.635 ms stddev 1.618
progress: 120.0 s, 2149.5 tps, lat 3.671 ms stddev 1.673
progress: 180.0 s, 2170.5 tps, lat 3.634 ms stddev 1.608
progress: 240.0 s, 2149.5 tps, lat 3.670 ms stddev 1.638
progress: 300.0 s, 2161.4 tps, lat 3.649 ms stddev 1.665
progress: 360.0 s, 2169.2 tps, lat 3.636 ms stddev 1.643
progress: 420.0 s, 2194.9 tps, lat 3.594 ms stddev 1.559
progress: 480.0 s, 2192.6 tps, lat 3.598 ms stddev 1.594
progress: 540.0 s, 2161.0 tps, lat 3.650 ms stddev 1.691
progress: 600.0 s, 2184.3 tps, lat 3.612 ms stddev 1.651
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 600 s
number of transactions actually processed: 1302173
latency average = 3.635 ms
latency stddev = 1.634 ms
initial connection time = 14.586 ms
tps = 2170.288785 (without initial connection time)
root@user-virtual-machine:~#

## Измерьте, какой объем журнальных файлов был сгенерирован за это время.

```
root@user-virtual-machine:~# sudo du -h /var/lib/postgresql/14/main/pg_wal
4,0K    /var/lib/postgresql/14/main/pg_wal/archive_status
113M    /var/lib/postgresql/14/main/pg_wal
root@user-virtual-machine:~#
```

## Оцените, какой объем приходится в среднем на одну контрольную точку.

На одну контрольную точку исходя из расчета: 

```
контрольная точка = 30 сек

нагрузочный тест = 600 сек

кол-во контрольных точек = нагрузочный тест / контрольную точку

Объем журнала = 113 Мб

Одна контрольная точка = Объем журнала / кол-во контрольных точек

Одна контрольная точка = 5,65 Мб
```

## Проверьте данные статистики: все ли контрольные точки выполнялись точно по расписанию. Почему так произошло?

Не все контрольные точки выполнились. По статистике среднее время выполнения контролькой точки 120 секунд.
Контрольные точки настроены на 30 секунд, и их выполнение накладывалось друг на друга.

## Сравните tps в синхронном/асинхронном режиме утилитой pgbench. Объясните полученный результат.

```
sudo -u postgres pgbench -P 1 -T 10 postgres
echo "synchronous_commit = off" | sudo tee -a /etc/postgresql/14/main/postgresql.conf
sudo systemctl restart postgresql
sudo -u postgres pgbench -P 1 -T 10 postgres
```

Среднее tps в синхронном режиме составляет 1293

Среднее время в асинхронном режиме составляет 1653

Разница составила в 361 транзакцию. Что составляет около 20-25%.

Причина в более эффективном сбрасывании на диск, теперь за вместо того что бы писать на диск каждый раз, все записываеться по расписанию и пачками.

## Создайте новый кластер с включенной контрольной суммой страниц. Создайте таблицу. Вставьте несколько значений. Выключите кластер. Измените пару байт в таблице. Включите кластер и сделайте выборку из таблицы. Что и почему произошло? Как проигнорировать ошибку и продолжить работу?

```
root@user-virtual-machine:~# sudo pg_createcluster 14 demo -p 5433 -- --data-checksums
root@user-virtual-machine:~# sudo pg_ctlcluster 14 demo start
root@user-virtual-machine:~# sudo -u postgres psql -p 5433 -c "create table messages(message text)"
root@user-virtual-machine:~# sudo -u postgres psql -p 5433 -c "insert into messages (message) values ('hello')"
root@user-virtual-machine:~# sudo -u postgres psql -p 5433 -c "insert into messages (message) values ('world')"
root@user-virtual-machine:~# sudo -u postgres psql -p 5433 -c "SELECT pg_relation_filepath('messages');" # base/13427/16384
root@user-virtual-machine:~# sudo pg_ctlcluster 14 demo stop
root@user-virtual-machine:~# sudo dd if=/dev/zero of=/var/lib/postgresql/14/demo/base/13427/16384 oflag=dsync conv=notrunc bs=1 count=8
root@user-virtual-machine:~# sudo pg_ctlcluster 14 demo start
root@user-virtual-machine:~# sudo -u postgres psql -p 5433 -c "select * from messages"
root@user-virtual-machine:~#
```

data checksums гарантирует целостность на уровне байтов в файлах и выводит ошибку о том что файл был поврежден

```
WARNING:  page verification failed, calculated checksum 40176 but expected 64197
ERROR:  invalid page in block 0 of relation base/13427/16384
```

Есть сразу несколько вариантов проигнорировать ошибку:

в самом сеансе можно попросить postgres игнорировать ошибку и выдывать что есть
найти поврежденные строки и удалить их
выставить настройку обнуляющую поврежденные строки и выполнить vacuum таблицы
SET zero_damaged_pages = on;
vacuum full messages;
select * from messages;


