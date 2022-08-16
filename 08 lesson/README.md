# MVCC, vacuum и autovacuum  
## создайте новый кластер PostgresSQL 13 (на выбор - GCE, CloudSQL) и установить на него PostgreSQL 13 с дефолтными настройками
```
root@user-virtual-machine:~# sudo apt update && sudo apt upgrade -y -q && sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo apt -y install postgresql-13
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

## применить параметры настройки PostgreSQL из прикрепленного к материалам занятия файла
 
откроем редактор nano в командной строке и применим настройки из файла урока к postgres

```
nano /etc/postgresql/13/main/postgresql.conf
```

```
max_connections = 40
shared_buffers = 1GB
effective_cache_size = 3GB
maintenance_work_mem = 512MB
checkpoint_completion_target = 0.9
wal_buffers = 16MB
default_statistics_target = 500
random_page_cost = 4
effective_io_concurrency = 2
work_mem = 6553kB
min_wal_size = 4GB
max_wal_size = 16GB
```

## выполнить pgbench -i postgres

```
root@user-virtual-machine:~# su - postgres
postgres@user-virtual-machine:~$ pgbench -i postgres
dropping old tables...
ЗАМЕЧАНИЕ:  таблица "pgbench_accounts" не существует, пропускается
ЗАМЕЧАНИЕ:  таблица "pgbench_branches" не существует, пропускается
ЗАМЕЧАНИЕ:  таблица "pgbench_history" не существует, пропускается
ЗАМЕЧАНИЕ:  таблица "pgbench_tellers" не существует, пропускается
creating tables...
generating data (client-side)...
100000 of 100000 tuples (100%) done (elapsed 0.15 s, remaining 0.00 s)
vacuuming...
creating primary keys...
done in 0.33 s (drop tables 0.00 s, create tables 0.02 s, client-side generate 0.23 s, vacuum 0.04 s, primary keys 0.03 s).
```

## запустить pgbench -c8 -P 60 -T 3600 -U postgres postgres

postgres@user-virtual-machine:~$ pgbench -c8 -P 60 -T 3600 -U postgres postgres
starting vacuum...end.

## дать отработать до конца

```
progress: 60.0 s, 2126.8 tps, lat 3.713 ms stddev 2.139
progress: 120.0 s, 2140.9 tps, lat 3.692 ms stddev 2.394
progress: 180.0 s, 2160.8 tps, lat 3.657 ms stddev 2.494
progress: 240.0 s, 2143.5 tps, lat 3.687 ms stddev 2.367
progress: 300.0 s, 2138.7 tps, lat 3.695 ms stddev 2.433
progress: 360.0 s, 2115.5 tps, lat 3.738 ms stddev 2.442
progress: 420.0 s, 2143.2 tps, lat 3.689 ms stddev 2.226
progress: 480.0 s, 2152.7 tps, lat 3.672 ms stddev 2.179
progress: 540.0 s, 2169.4 tps, lat 3.643 ms stddev 1.740
progress: 600.0 s, 2165.0 tps, lat 3.652 ms stddev 1.758
progress: 660.0 s, 2159.0 tps, lat 3.661 ms stddev 1.732
progress: 720.0 s, 2167.0 tps, lat 3.648 ms stddev 1.733
progress: 780.0 s, 2151.7 tps, lat 3.675 ms stddev 1.791
progress: 840.0 s, 2150.9 tps, lat 3.675 ms stddev 1.754
progress: 900.0 s, 2153.9 tps, lat 3.670 ms stddev 1.737
progress: 960.0 s, 2153.1 tps, lat 3.673 ms stddev 1.753
progress: 1020.0 s, 2163.6 tps, lat 3.653 ms stddev 1.725
progress: 1080.0 s, 2173.4 tps, lat 3.636 ms stddev 1.721
progress: 1140.0 s, 2197.3 tps, lat 3.595 ms stddev 1.697
progress: 1200.0 s, 2192.3 tps, lat 3.605 ms stddev 1.718
progress: 1260.0 s, 2168.2 tps, lat 3.645 ms stddev 1.752
progress: 1320.0 s, 2192.4 tps, lat 3.605 ms stddev 1.706
progress: 1380.0 s, 2126.4 tps, lat 3.713 ms stddev 1.747
progress: 1440.0 s, 2195.3 tps, lat 3.599 ms stddev 1.690
progress: 1500.0 s, 2189.2 tps, lat 3.609 ms stddev 1.705
progress: 1560.0 s, 2173.4 tps, lat 3.636 ms stddev 1.727
progress: 1620.0 s, 2182.8 tps, lat 3.620 ms stddev 1.708
progress: 1680.0 s, 2202.1 tps, lat 3.588 ms stddev 1.703
progress: 1740.0 s, 2198.3 tps, lat 3.595 ms stddev 1.706
progress: 1800.0 s, 2198.5 tps, lat 3.593 ms stddev 1.694
progress: 1860.0 s, 2193.8 tps, lat 3.602 ms stddev 1.707
progress: 1920.0 s, 2208.2 tps, lat 3.580 ms stddev 1.686
progress: 1980.0 s, 2196.5 tps, lat 3.597 ms stddev 1.711
progress: 2040.0 s, 2204.4 tps, lat 3.584 ms stddev 1.714
progress: 2100.0 s, 2191.0 tps, lat 3.606 ms stddev 1.730
progress: 2160.0 s, 2179.9 tps, lat 3.626 ms stddev 1.724
progress: 2220.0 s, 2187.5 tps, lat 3.613 ms stddev 1.706
progress: 2280.0 s, 2182.4 tps, lat 3.622 ms stddev 1.773
progress: 2340.0 s, 2161.4 tps, lat 3.656 ms stddev 1.724
progress: 2400.0 s, 2170.7 tps, lat 3.642 ms stddev 1.714
progress: 2460.0 s, 2184.5 tps, lat 3.619 ms stddev 1.738
progress: 2520.0 s, 2174.4 tps, lat 3.633 ms stddev 1.715
progress: 2580.0 s, 2173.4 tps, lat 3.636 ms stddev 1.739
progress: 2640.0 s, 2200.4 tps, lat 3.591 ms stddev 1.692
progress: 2700.0 s, 2185.5 tps, lat 3.615 ms stddev 1.708
progress: 2760.0 s, 2183.7 tps, lat 3.619 ms stddev 1.737
progress: 2820.0 s, 2180.9 tps, lat 3.624 ms stddev 1.720
progress: 2880.0 s, 2165.3 tps, lat 3.650 ms stddev 1.729
progress: 2940.0 s, 2178.0 tps, lat 3.628 ms stddev 1.703
progress: 3000.0 s, 2193.8 tps, lat 3.603 ms stddev 1.707
progress: 3060.0 s, 2193.9 tps, lat 3.602 ms stddev 1.681
progress: 3120.0 s, 2172.5 tps, lat 3.638 ms stddev 1.719
progress: 3180.0 s, 2160.2 tps, lat 3.659 ms stddev 1.747
progress: 3240.0 s, 2184.2 tps, lat 3.617 ms stddev 1.707
progress: 3300.0 s, 2200.6 tps, lat 3.590 ms stddev 1.677
progress: 3360.0 s, 2198.0 tps, lat 3.593 ms stddev 1.690
progress: 3420.0 s, 2186.6 tps, lat 3.613 ms stddev 1.685
progress: 3480.0 s, 2185.7 tps, lat 3.616 ms stddev 1.716
progress: 3540.0 s, 2157.0 tps, lat 3.664 ms stddev 1.739
progress: 3600.0 s, 2167.8 tps, lat 3.645 ms stddev 1.723
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 3600 s
number of transactions actually processed: 7826863
latency average = 3.635 ms
latency stddev = 1.814 ms
tps = 2174.116848 (including connections establishing)
tps = 2174.117841 (excluding connections establishing)
postgres@user-virtual-machine:~$
```

## зафиксировать среднее значение tps в последней ⅙ части работы

```
среднее значение tps = 2180
```

## настроить autovacuum максимально эффективно

Учитывая что параметры в файле для ДЗ даны под HDD а в системе используеться NVMe SSD, попробуем перенастроить параметры влияющие на это а именно 

```
random_page_cost = 1.1
effective_io_concurrency = 200
```

Исходя из корректировки и результата: 

```
postgres@user-virtual-machine:~$ pgbench -c8 -P 60 -T 3600 -U postgres postgres
starting vacuum...end.
progress: 60.0 s, 2167.7 tps, lat 3.644 ms stddev 1.789
progress: 120.0 s, 2153.1 tps, lat 3.671 ms stddev 1.842
progress: 180.0 s, 2146.8 tps, lat 3.682 ms stddev 1.866
progress: 240.0 s, 2185.9 tps, lat 3.616 ms stddev 1.702
progress: 300.0 s, 2178.0 tps, lat 3.629 ms stddev 1.708
progress: 360.0 s, 2181.3 tps, lat 3.622 ms stddev 1.714
progress: 420.0 s, 2149.5 tps, lat 3.677 ms stddev 1.832
progress: 480.0 s, 2188.8 tps, lat 3.611 ms stddev 1.765
progress: 540.0 s, 2188.4 tps, lat 3.611 ms stddev 1.782
progress: 600.0 s, 2185.0 tps, lat 3.616 ms stddev 1.724
progress: 660.0 s, 2173.3 tps, lat 3.637 ms stddev 1.742
progress: 720.0 s, 2178.7 tps, lat 3.627 ms stddev 1.731
progress: 780.0 s, 2176.4 tps, lat 3.633 ms stddev 1.734
progress: 840.0 s, 2175.1 tps, lat 3.634 ms stddev 1.717
progress: 900.0 s, 2191.7 tps, lat 3.608 ms stddev 1.702
progress: 960.0 s, 2177.9 tps, lat 3.631 ms stddev 1.739
progress: 1020.0 s, 2188.7 tps, lat 3.610 ms stddev 1.710
progress: 1080.0 s, 2099.3 tps, lat 3.764 ms stddev 1.994
progress: 1140.0 s, 2151.0 tps, lat 3.670 ms stddev 1.790
progress: 1200.0 s, 2171.2 tps, lat 3.637 ms stddev 1.730
progress: 1260.0 s, 2158.8 tps, lat 3.658 ms stddev 1.825
progress: 1320.0 s, 2169.9 tps, lat 3.638 ms stddev 1.715
progress: 1380.0 s, 2155.8 tps, lat 3.664 ms stddev 1.759
progress: 1440.0 s, 2126.1 tps, lat 3.715 ms stddev 1.806
progress: 1500.0 s, 2175.6 tps, lat 3.634 ms stddev 1.728
progress: 1560.0 s, 2163.8 tps, lat 3.651 ms stddev 1.759
progress: 1620.0 s, 2164.2 tps, lat 3.651 ms stddev 1.745
progress: 1680.0 s, 2164.8 tps, lat 3.652 ms stddev 1.781
progress: 1740.0 s, 2167.0 tps, lat 3.647 ms stddev 1.793
progress: 1800.0 s, 2179.6 tps, lat 3.625 ms stddev 1.724
progress: 1860.0 s, 2156.6 tps, lat 3.665 ms stddev 1.787
progress: 1920.0 s, 2176.5 tps, lat 3.629 ms stddev 1.720
progress: 1980.0 s, 2207.2 tps, lat 3.580 ms stddev 1.690
progress: 2040.0 s, 2200.1 tps, lat 3.591 ms stddev 1.675
progress: 2100.0 s, 2203.5 tps, lat 3.586 ms stddev 1.706
progress: 2160.0 s, 2210.5 tps, lat 3.575 ms stddev 1.687
progress: 2220.0 s, 2191.7 tps, lat 3.605 ms stddev 1.701
progress: 2280.0 s, 2184.8 tps, lat 3.617 ms stddev 1.758
progress: 2340.0 s, 2181.9 tps, lat 3.622 ms stddev 1.721
progress: 2400.0 s, 2190.0 tps, lat 3.610 ms stddev 1.716
progress: 2460.0 s, 2167.0 tps, lat 3.647 ms stddev 1.757
progress: 2520.0 s, 2184.1 tps, lat 3.618 ms stddev 1.708
progress: 2580.0 s, 2200.2 tps, lat 3.591 ms stddev 1.689
progress: 2640.0 s, 2214.1 tps, lat 3.568 ms stddev 1.676
progress: 2700.0 s, 2198.6 tps, lat 3.595 ms stddev 1.734
progress: 2760.0 s, 2188.9 tps, lat 3.611 ms stddev 1.715
progress: 2820.0 s, 2176.9 tps, lat 3.630 ms stddev 1.697
progress: 2880.0 s, 2172.9 tps, lat 3.636 ms stddev 1.726
progress: 2940.0 s, 2187.7 tps, lat 3.612 ms stddev 1.745
progress: 3000.0 s, 2197.8 tps, lat 3.595 ms stddev 1.706
progress: 3060.0 s, 2181.6 tps, lat 3.623 ms stddev 1.707
progress: 3120.0 s, 2167.3 tps, lat 3.646 ms stddev 1.722
progress: 3180.0 s, 2177.9 tps, lat 3.628 ms stddev 1.719
progress: 3240.0 s, 2182.6 tps, lat 3.621 ms stddev 1.709
progress: 3300.0 s, 2183.6 tps, lat 3.619 ms stddev 1.716
progress: 3360.0 s, 2191.5 tps, lat 3.607 ms stddev 1.691
progress: 3420.0 s, 2162.7 tps, lat 3.653 ms stddev 1.733
progress: 3480.0 s, 2174.4 tps, lat 3.635 ms stddev 1.717
progress: 3540.0 s, 2198.7 tps, lat 3.594 ms stddev 1.701
progress: 3600.0 s, 2202.5 tps, lat 3.587 ms stddev 1.702
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 3600 s
number of transactions actually processed: 7838834
latency average = 3.629 ms
latency stddev = 1.740 ms
tps = 2177.440535 (including connections establishing)
tps = 2177.441851 (excluding connections establishing)
postgres@user-virtual-machine:~$
```

tps в среднем стал на еденицу больше и эффективность повысилась незаметно

## так чтобы получить максимально ровное значение tps на горизонте часа

```
postgres@user-virtual-machine:~$ pgbench -c8 -P 60 -T 3600 -U postgres postgres
starting vacuum...end.
progress: 60.0 s, 2161.8 tps, lat 3.655 ms stddev 1.790
progress: 120.0 s, 2184.8 tps, lat 3.617 ms stddev 1.715
progress: 180.0 s, 2167.1 tps, lat 3.646 ms stddev 1.738
progress: 240.0 s, 2167.2 tps, lat 3.647 ms stddev 1.822
progress: 300.0 s, 2135.8 tps, lat 3.699 ms stddev 1.825
progress: 360.0 s, 2170.6 tps, lat 3.641 ms stddev 1.749
progress: 420.0 s, 2142.8 tps, lat 3.687 ms stddev 1.842
progress: 480.0 s, 2134.1 tps, lat 3.702 ms stddev 1.813
progress: 540.0 s, 2105.6 tps, lat 3.750 ms stddev 1.934
progress: 600.0 s, 2153.2 tps, lat 3.669 ms stddev 1.871
progress: 660.0 s, 2149.8 tps, lat 3.674 ms stddev 1.872
progress: 720.0 s, 2165.1 tps, lat 3.649 ms stddev 1.797
progress: 780.0 s, 2135.5 tps, lat 3.699 ms stddev 1.914
progress: 840.0 s, 2165.2 tps, lat 3.648 ms stddev 1.795
progress: 900.0 s, 2144.2 tps, lat 3.683 ms stddev 1.812
progress: 960.0 s, 2130.9 tps, lat 3.707 ms stddev 1.963
progress: 1020.0 s, 2185.9 tps, lat 3.615 ms stddev 1.711
progress: 1080.0 s, 2170.9 tps, lat 3.639 ms stddev 1.717
progress: 1140.0 s, 2173.9 tps, lat 3.635 ms stddev 1.731
progress: 1200.0 s, 2158.8 tps, lat 3.662 ms stddev 1.742
progress: 1260.0 s, 2162.6 tps, lat 3.654 ms stddev 1.743
progress: 1320.0 s, 2185.2 tps, lat 3.617 ms stddev 1.712
progress: 1380.0 s, 2153.1 tps, lat 3.668 ms stddev 1.727
progress: 1440.0 s, 2179.0 tps, lat 3.626 ms stddev 1.715
progress: 1500.0 s, 2176.5 tps, lat 3.630 ms stddev 1.730
progress: 1560.0 s, 2161.2 tps, lat 3.656 ms stddev 1.758
progress: 1620.0 s, 2168.6 tps, lat 3.645 ms stddev 1.716
progress: 1680.0 s, 2175.2 tps, lat 3.632 ms stddev 1.709
progress: 1740.0 s, 2170.4 tps, lat 3.641 ms stddev 1.728
progress: 1800.0 s, 2171.0 tps, lat 3.638 ms stddev 1.736
progress: 1860.0 s, 2148.0 tps, lat 3.678 ms stddev 1.737
progress: 1920.0 s, 2182.3 tps, lat 3.621 ms stddev 1.699
progress: 1980.0 s, 2157.3 tps, lat 3.663 ms stddev 1.738
progress: 2040.0 s, 2156.6 tps, lat 3.663 ms stddev 1.727
progress: 2100.0 s, 2157.9 tps, lat 3.662 ms stddev 1.732
progress: 2160.0 s, 2162.7 tps, lat 3.655 ms stddev 1.746
progress: 2220.0 s, 2163.0 tps, lat 3.654 ms stddev 1.729
progress: 2280.0 s, 2176.6 tps, lat 3.632 ms stddev 1.728
progress: 2340.0 s, 2194.7 tps, lat 3.600 ms stddev 1.703
progress: 2400.0 s, 2191.5 tps, lat 3.604 ms stddev 1.682
progress: 2460.0 s, 2157.7 tps, lat 3.662 ms stddev 1.733
progress: 2520.0 s, 2171.0 tps, lat 3.640 ms stddev 1.720
progress: 2580.0 s, 2189.6 tps, lat 3.612 ms stddev 1.711
progress: 2640.0 s, 2166.9 tps, lat 3.649 ms stddev 1.739
progress: 2700.0 s, 2166.2 tps, lat 3.648 ms stddev 1.745
progress: 2760.0 s, 2160.1 tps, lat 3.659 ms stddev 1.729
progress: 2820.0 s, 2179.4 tps, lat 3.627 ms stddev 1.718
progress: 2880.0 s, 2183.5 tps, lat 3.620 ms stddev 1.734
progress: 2940.0 s, 2173.8 tps, lat 3.636 ms stddev 1.719
progress: 3000.0 s, 2184.9 tps, lat 3.617 ms stddev 1.716
progress: 3060.0 s, 2171.8 tps, lat 3.637 ms stddev 1.721
progress: 3120.0 s, 2171.8 tps, lat 3.639 ms stddev 1.728
progress: 3180.0 s, 2176.7 tps, lat 3.632 ms stddev 1.734
progress: 3240.0 s, 2181.6 tps, lat 3.623 ms stddev 1.708
progress: 3300.0 s, 2171.7 tps, lat 3.639 ms stddev 1.739
progress: 3360.0 s, 2175.3 tps, lat 3.634 ms stddev 1.743
progress: 3420.0 s, 2168.6 tps, lat 3.644 ms stddev 1.723
progress: 3480.0 s, 2180.9 tps, lat 3.624 ms stddev 1.719
progress: 3540.0 s, 2186.1 tps, lat 3.614 ms stddev 1.694
progress: 3600.0 s, 2194.8 tps, lat 3.601 ms stddev 1.709
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 3600 s
number of transactions actually processed: 7800568
latency average = 3.647 ms
latency stddev = 1.753 ms
tps = 2166.815713 (including connections establishing)
tps = 2166.816968 (excluding connections establishing)
postgres@user-virtual-machine:~$
```

Разблокировка значений autovacuum не принесла ощутимых результатов в файле настройки. Кол-во транзакций в среднем значении упало на 11 едениц. 
Не ясно, по каким причинам так получилось. В целом осталось не ясным как работает оптимизация, и почему от дополнительно настороенного процеса для оптимизации стало только хуже ...