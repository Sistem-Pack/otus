# Логический уровень PostgreSQL 
## создайте новый кластер PostgresSQL 13 (на выбор - GCE, CloudSQL)
```
root@user-virtual-machine:~# root@user-virtual-machine:~# sudo apt update && sudo apt upgrade -y -q && sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get updatgresql-13
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease
Сущ:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease
Сущ:4 http://security.ubuntu.com/ubuntu focal-security InRelease
Чтение списков пакетов… Готово
Построение дерева зависимостей
Чтение информации о состоянии… Готово
Все пакеты имеют последние версии.
Чтение списков пакетов…
Построение дерева зависимостей…
Чтение информации о состоянии…
Расчёт обновлений…
Следующий пакет устанавливался автоматически и больше не требуется:
  libfwupdplugin1
Для его удаления используйте «sudo apt autoremove».
Обновлено 0 пакетов, установлено 0 новых пакетов, для удаления отмечено 0 пакетов, и 0 пакетов не обновлено.
OK
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease
Сущ:3 http://security.ubuntu.com/ubuntu focal-security InRelease
Сущ:4 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease
Пол:5 http://apt.postgresql.org/pub/repos/apt focal-pgdg InRelease [91,7 kB]
Пол:6 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 Packages [240 kB]
Получено 332 kB за 1с (320 kB/s)
Чтение списков пакетов… Готово
N: Пропускается получение настроенного файла «main/binary-i386/Packages», так как репозиторий «http://apt.postgresql.org/pub/repos/apt focal-pgdg InRelease» не поддерживает архитектуру «i386»
Чтение списков пакетов… Готово
Построение дерева зависимостей
Чтение информации о состоянии… Готово
Следующий пакет устанавливался автоматически и больше не требуется:
  libfwupdplugin1
Для его удаления используйте «sudo apt autoremove».
Будут установлены следующие дополнительные пакеты:
  libcommon-sense-perl libjson-perl libjson-xs-perl libllvm10 libpq5 libtypes-serialiser-perl pgdg-keyring postgresql-client-13 postgresql-client-common postgresql-common
  sysstat
Предлагаемые пакеты:
  postgresql-doc-13 isag
Следующие НОВЫЕ пакеты будут установлены:
  libcommon-sense-perl libjson-perl libjson-xs-perl libllvm10 libpq5 libtypes-serialiser-perl pgdg-keyring postgresql-13 postgresql-client-13 postgresql-client-common
  postgresql-common sysstat
Обновлено 0 пакетов, установлено 12 новых пакетов, для удаления отмечено 0 пакетов, и 0 пакетов не обновлено.
Необходимо скачать 33,1 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 133 MB.
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libcommon-sense-perl amd64 3.74-2build6 [20,1 kB]
Пол:2 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 libpq5 amd64 14.4-1.pgdg20.04+1 [172 kB]
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libjson-perl all 4.02000-2 [80,9 kB]
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libtypes-serialiser-perl all 1.0-1 [12,1 kB]
Пол:5 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libjson-xs-perl amd64 4.020-1build1 [83,7 kB]
Пол:6 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libllvm10 amd64 1:10.0.0-4ubuntu1 [15,3 MB]
Пол:7 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 pgdg-keyring all 2018.2 [10,7 kB]
Пол:8 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-client-common all 241.pgdg20.04+1 [92,1 kB]
Пол:9 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-client-13 amd64 13.7-1.pgdg20.04+1 [1 512 kB]
Пол:10 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-common all 241.pgdg20.04+1 [230 kB]
Пол:11 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-13 amd64 13.7-1.pgdg20.04+1 [15,1 MB]
Пол:12 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 sysstat amd64 12.2.0-2ubuntu0.1 [448 kB]
Получено 33,1 MB за 13с (2 490 kB/s)
Предварительная настройка пакетов …
Выбор ранее не выбранного пакета libcommon-sense-perl.
(Чтение базы данных … на данный момент установлено 161599 файлов и каталогов.)
Подготовка к распаковке …/00-libcommon-sense-perl_3.74-2build6_amd64.deb …
Распаковывается libcommon-sense-perl (3.74-2build6) …
Выбор ранее не выбранного пакета libjson-perl.
Подготовка к распаковке …/01-libjson-perl_4.02000-2_all.deb …
Распаковывается libjson-perl (4.02000-2) …
Выбор ранее не выбранного пакета libtypes-serialiser-perl.
Подготовка к распаковке …/02-libtypes-serialiser-perl_1.0-1_all.deb …
Распаковывается libtypes-serialiser-perl (1.0-1) …
Выбор ранее не выбранного пакета libjson-xs-perl.
Подготовка к распаковке …/03-libjson-xs-perl_4.020-1build1_amd64.deb …
Распаковывается libjson-xs-perl (4.020-1build1) …
Выбор ранее не выбранного пакета libllvm10:amd64.
Подготовка к распаковке …/04-libllvm10_1%3a10.0.0-4ubuntu1_amd64.deb …
Распаковывается libllvm10:amd64 (1:10.0.0-4ubuntu1) …
Выбор ранее не выбранного пакета libpq5:amd64.
Подготовка к распаковке …/05-libpq5_14.4-1.pgdg20.04+1_amd64.deb …
Распаковывается libpq5:amd64 (14.4-1.pgdg20.04+1) …
Выбор ранее не выбранного пакета pgdg-keyring.
Подготовка к распаковке …/06-pgdg-keyring_2018.2_all.deb …
Распаковывается pgdg-keyring (2018.2) …
Выбор ранее не выбранного пакета postgresql-client-common.
Подготовка к распаковке …/07-postgresql-client-common_241.pgdg20.04+1_all.deb …
Распаковывается postgresql-client-common (241.pgdg20.04+1) …
Выбор ранее не выбранного пакета postgresql-client-13.
Подготовка к распаковке …/08-postgresql-client-13_13.7-1.pgdg20.04+1_amd64.deb …
Распаковывается postgresql-client-13 (13.7-1.pgdg20.04+1) …
Выбор ранее не выбранного пакета postgresql-common.
Подготовка к распаковке …/09-postgresql-common_241.pgdg20.04+1_all.deb …
Добавляется «отклонение /usr/bin/pg_config в /usr/bin/pg_config.libpq-dev из-за postgresql-common»
Распаковывается postgresql-common (241.pgdg20.04+1) …
Выбор ранее не выбранного пакета postgresql-13.
Подготовка к распаковке …/10-postgresql-13_13.7-1.pgdg20.04+1_amd64.deb …
Распаковывается postgresql-13 (13.7-1.pgdg20.04+1) …
Выбор ранее не выбранного пакета sysstat.
Подготовка к распаковке …/11-sysstat_12.2.0-2ubuntu0.1_amd64.deb …
Распаковывается sysstat (12.2.0-2ubuntu0.1) …
Настраивается пакет pgdg-keyring (2018.2) …
Removing apt.postgresql.org key from trusted.gpg: OK
Настраивается пакет libpq5:amd64 (14.4-1.pgdg20.04+1) …
Настраивается пакет libcommon-sense-perl (3.74-2build6) …
Настраивается пакет libllvm10:amd64 (1:10.0.0-4ubuntu1) …
Настраивается пакет libtypes-serialiser-perl (1.0-1) …
Настраивается пакет libjson-perl (4.02000-2) …
Настраивается пакет sysstat (12.2.0-2ubuntu0.1) …

Creating config file /etc/default/sysstat with new version
update-alternatives: используется /usr/bin/sar.sysstat для предоставления /usr/bin/sar (sar) в автоматическом режиме
Created symlink /etc/systemd/system/multi-user.target.wants/sysstat.service → /lib/systemd/system/sysstat.service.
Настраивается пакет postgresql-client-common (241.pgdg20.04+1) …
Настраивается пакет libjson-xs-perl (4.020-1build1) …
Настраивается пакет postgresql-client-13 (13.7-1.pgdg20.04+1) …
update-alternatives: используется /usr/share/postgresql/13/man/man1/psql.1.gz для предоставления /usr/share/man/man1/psql.1.gz (psql.1.gz) в автоматическом режиме
Настраивается пакет postgresql-common (241.pgdg20.04+1) …
Добавление пользователя postgres в группу ssl-cert

Creating config file /etc/postgresql-common/createcluster.conf with new version
Building PostgreSQL dictionaries from installed myspell/hunspell packages...
  en_us
Removing obsolete dictionary files:
Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /lib/systemd/system/postgresql.service.
Настраивается пакет postgresql-13 (13.7-1.pgdg20.04+1) …
Creating new PostgreSQL cluster 13/main ...
/usr/lib/postgresql/13/bin/initdb -D /var/lib/postgresql/13/main --auth-local peer --auth-host md5
Файлы, относящиеся к этой СУБД, будут принадлежать пользователю "postgres".
От его имени также будет запускаться процесс сервера.

Кластер баз данных будет инициализирован с локалью "ru_RU.UTF-8".
Кодировка БД по умолчанию, выбранная в соответствии с настройками: "UTF8".
Выбрана конфигурация текстового поиска по умолчанию "russian".

Контроль целостности страниц данных отключён.

исправление прав для существующего каталога /var/lib/postgresql/13/main... ок
создание подкаталогов... ок
выбирается реализация динамической разделяемой памяти... posix
выбирается значение max_connections по умолчанию... 100
выбирается значение shared_buffers по умолчанию... 128MB
выбирается часовой пояс по умолчанию... Asia/Omsk
создание конфигурационных файлов... ок
выполняется подготовительный скрипт... ок
выполняется заключительная инициализация... ок
сохранение данных на диске... ок

Готово. Теперь вы можете запустить сервер баз данных:

    pg_ctlcluster 13 main start

update-alternatives: используется /usr/share/postgresql/13/man/man1/postmaster.1.gz для предоставления /usr/share/man/man1/postmaster.1.gz (postmaster.1.gz) в автоматическом режиме
Обрабатываются триггеры для systemd (245.4-4ubuntu3.17) …
Обрабатываются триггеры для man-db (2.9.1-1) …
Обрабатываются триггеры для libc-bin (2.31-0ubuntu9.9) …
root@user-virtual-machine:~#
```

Запустим кластер pg_ctlcluster 13 main start
```
root@user-virtual-machine:~# pg_ctlcluster 13 main start
```
проверим что кластер работает
```
root@user-virtual-machine:~# sudo -u postgres pg_lsclusters
Ver Cluster Port Status Owner    Data directory              Log file
13  main    5432 online postgres /var/lib/postgresql/13/main /var/log/postgresql/postgresql-13-main.log
```
## зайдите в созданный кластер под пользователем postgres
```
root@user-virtual-machine:~# sudo -u postgres psql -p 5432
could not change directory to "/root": Отказано в доступе
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
Type "help" for help.

postgres=#
```

## создайте новую базу данных testdb

```
postgres=# create database testdb
postgres-# ;
CREATE DATABASE
postgres=#
```

## зайдите в созданную базу данных под пользователем postgres

```
You are now connected to database "testdb" as user "postgres".
testdb=#
```
## создайте новую схему testnm
```
testdb=#  CREATE SCHEMA testnm;
CREATE SCHEMA
testdb=#
```
## создайте новую таблицу t1 с одной колонкой c1 типа integer
```
testdb=# CREATE TABLE t1(c1 integer);
CREATE TABLE
testdb=#
```
## вставьте строку со значением c1=1
```
testdb=# INSERT INTO t1 values(1);
INSERT 0 1
testdb=#
```
## создайте новую роль readonly
```
testdb=# CREATE role readonly;
CREATE ROLE
testdb=#
```
## дайте новой роли право на подключение к базе данных testdb
```
testdb=# GRANT CONNECT ON DATABASE TESTDB TO READONLY;
GRANT
testdb=#
```
## дайте новой роли право на использование схемы testnm

```
testdb=# GRANT USAGE ON SCHEMA TESTNM TO READONLY;
GRANT
testdb=#
```
## дайте новой роли право на select для всех таблиц схемы testnm
```
testdb=# GRANT SELECT ON ALL TABLES IN SCHEMA TESTNM TO READONLY;
GRANT
testdb=#
```

##  создайте пользователя testread с паролем test123
```
testdb=# CREATE USER TESTREAD WITH PASSWORD 'TEST123';
CREATE ROLE
testdb=#
```
## дайте роль readonly пользователю testread
```
testdb=# GRANT READONLY TO TESTREAD;
GRANT ROLE
testdb=#
```

## зайдите под пользователем testread в базу данных testdb

```
root@user-virtual-machine:~# psql -h 127.0.0.1 -U testread -d testdb -W
Пароль:
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
SSL-соединение (протокол: TLSv1.3, шифр: TLS_AES_256_GCM_SHA384, бит: 256, сжатие: выкл.)
Введите "help", чтобы получить справку.

testdb=>
```

## сделайте select * from t1;

```
testdb=> SELECT * FROM t1;
ОШИБКА:  нет доступа к таблице t1
testdb=>
```
## получилось? (могло если вы делали сами не по шпаргалке и не упустили один существенный момент про который позже)
нет
## напишите что именно произошло в тексте домашнего задания
## у вас есть идеи почему? ведь права то дали?
## посмотрите на список таблиц
```
testdb=> \dt
         Список отношений
 Схема  | Имя |   Тип   | Владелец
--------+-----+---------+----------
 public | t1  | таблица | postgres
(1 строка)

testdb=>
```
## подсказка в шпаргалке под пунктом 20
```
таблица создана в схеме public а не testnm и прав на public для роли readonly не давали
```
## а почему так получилось с таблицей (если делали сами и без шпаргалки то может у вас все нормально)
```
Делал без шпаргалки(её еще необходимо было увидеть как оказалось). Просто не внимательно следовал заданию.
```
## вернитесь в базу данных testdb под пользователем postgres

```
root@user-virtual-machine:~# sudo -u postgres psql -p 5432
could not change directory to "/root": Отказано в доступе
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
Type "help" for help.

postgres=#
```

## удалите таблицу t1
```
postgres=# \c testdb
You are now connected to database "testdb" as user "postgres".
testdb=# drop table t1;
DROP TABLE
testdb=#
```
## создайте ее заново но уже с явным указанием имени схемы testnm
```
testdb=# create table testnm.t1(c integer);
CREATE TABLE
testdb=#
```
##  вставьте строку со значением c1=1

```
testdb=# insert into testnm.t1 values (1);
INSERT 0 1
testdb=#
```
## зайдите под пользователем testread в базу данных testdb

```
root@user-virtual-machine:~# \q
root@user-virtual-machine:~# psql -h 127.0.0.1 -U testread -d testdb -W
Пароль:
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
SSL-соединение (протокол: TLSv1.3, шифр: TLS_AES_256_GCM_SHA384, бит: 256, сжатие: выкл.)
Введите "help", чтобы получить справку.

testdb=>
```
## сделайте select * from testnm.t1;

```
testdb=> select * from testnm.t1;
ОШИБКА:  нет доступа к таблице t1
testdb=>
```

##  получилось?
```
нет
```
## есть идеи почему? если нет - смотрите шпаргалку
```
Да, необходимо дать права пользователю на выборку данных из таблицы
```

## как сделать так чтобы такое больше не повторялось? если нет идей - смотрите шпаргалку

```
root@user-virtual-machine:~# sudo -u postgres psql -p 5432
could not change directory to "/root": Отказано в доступе
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
Type "help" for help.

postgres=# \c testdb
You are now connected to database "testdb" as user "postgres".
testdb=# ALTER DEFAULT PRIVILEGES IN SCHEMA TESTNM GRANT SELECT ON TABLES TO READONLY;
ALTER DEFAULT PRIVILEGES
testdb=# \q
root@user-virtual-machine:~# psql -h 127.0.0.1 -U testread -d testdb -W
Пароль:
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
SSL-соединение (протокол: TLSv1.3, шифр: TLS_AES_256_GCM_SHA384, бит: 256, сжатие: выкл.)
Введите "help", чтобы получить справку.
```
## сделайте select * from testnm.t1;
```
select * from testnm.t1;
```
## получилось?
```
нет
```
## есть идеи почему? если нет - смотрите шпаргалку
```
идей нет, смотрим шпаргалку

root@user-virtual-machine:~# sudo -u postgres psql -p 5432
could not change directory to "/root": Отказано в доступе
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
Type "help" for help.

postgres=# \c testdb
You are now connected to database "testdb" as user "postgres".
testdb=# grant select on testnm.t1 to readonly;
GRANT
testdb=# \q
root@user-virtual-machine:~#
root@user-virtual-machine:~# psql -h 127.0.0.1 -U testread -d testdb -W
Пароль:
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
SSL-соединение (протокол: TLSv1.3, шифр: TLS_AES_256_GCM_SHA384, бит: 256, сжатие: выкл.)
Введите "help", чтобы получить справку.

testdb=>
```
## сделайте select * from testnm.t1;
```
testdb=> select * from testnm.t1;
 c
---
 1
(1 строка)
```
## получилось?
```
Да
```
## Ура! 
```

```

## теперь попробуйте выполнить команду create table t2(c1 integer); insert into t2 values (2);
```
testdb=> create table t2(c1 integer);
CREATE TABLE
testdb=>

testdb=> insert into t2 values (2);
INSERT 0 1
testdb=>
```
## а как так? нам же никто прав на создание таблиц и insert в них под ролью readonly?

Ответ
```
testdb=> \dt
         Список отношений
 Схема  | Имя |   Тип   | Владелец
--------+-----+---------+----------
 public | t2  | таблица | testread
(1 строка)
```

## есть идеи как убрать эти права? если нет - смотрите шпаргалку
```
нет
```
## если вы справились сами то расскажите что сделали и почему, если смотрели шпаргалку - объясните что сделали и почему выполнив указанные в ней команды

```
Зайдем под пользователем postgres и удалим права в базе public

root@user-virtual-machine:~# sudo -u postgres psql -p 5432
could not change directory to "/root": Отказано в доступе
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
Type "help" for help.

postgres=#

postgres=# REVOKE CREATE on SCHEMA public FROM public;
REVOKE
postgres=#

postgres=# REVOKE ALL ON DATABASE testdb FROM public;
REVOKE
postgres=#

root@user-virtual-machine:~# psql -h 127.0.0.1 -U testread -d testdb -W
Пароль:
psql (13.7 (Ubuntu 13.7-1.pgdg20.04+1))
SSL-соединение (протокол: TLSv1.3, шифр: TLS_AES_256_GCM_SHA384, бит: 256, сжатие: выкл.)
Введите "help", чтобы получить справку.

testdb=>
```

##  теперь попробуйте выполнить команду create table t3(c1 integer); insert into t2 values (2);
```
testdb=> create table t3(c1 integer);
CREATE TABLE
testdb=> insert into t2 values (2);
INSERT 0 1
testdb=>
```

## расскажите что получилось и почему 
```
Удалось создать новую таблицу и внести данные в другую. Так как права пользователю были правильно разданы и успешно отработали GRANT и REVOKE. 
Решилась проблема с дефолтной схемой public созданной в БД по умолчанию для данного пользователя.
```
