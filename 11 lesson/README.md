# Настройка PostgreSQL 

## развернуть виртуальную машину любым удобным способом

```
сделано
```

## поставить на неё PostgreSQL 14 любым способом

```
root@user-virtual-machine:~# sudo apt update && sudo apt upgrade -y -q && sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo apt -y install postgresql-14
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://security.ubuntu.com/ubuntu focal-security InRelease
Сущ:3 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease
Сущ:4 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease
Чтение списков пакетов… Готово
Построение дерева зависимостей
Чтение информации о состоянии… Готово
Может быть обновлено 8 пакетов. Запустите «apt list --upgradable» для их показа.
Чтение списков пакетов…
Построение дерева зависимостей…
Чтение информации о состоянии…
Расчёт обновлений…
Следующий пакет устанавливался автоматически и больше не требуется:
  libfwupdplugin1
Для его удаления используйте «sudo apt autoremove».
Следующие пакеты будут обновлены:
  libgstreamer-plugins-bad1.0-0 libnetplan0 libsnmp-base libsnmp35 linux-firmware netplan.io tracker-extract
  tracker-miner-fs
Обновлено 8 пакетов, установлено 0 новых пакетов, для удаления отмечено 0 пакетов, и 0 пакетов не обновлено.
Необходимо скачать 127 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 70,7 kB.
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 netplan.io amd64 0.104-0ubuntu2~20.04.2 [88,0 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libnetplan0 amd64 0.104-0ubuntu2~20.04.2 [82,5 kB]
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libsnmp-base all 5.8+dfsg-2ubuntu2.5 [206 kB]
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libsnmp35 amd64 5.8+dfsg-2ubuntu2.5 [980 kB]
Пол:5 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 linux-firmware all 1.187.33 [125 MB]

Пол:6 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 tracker-miner-fs amd64 2.3.3-2ubuntu0.20.04.1 [68,3 kB]
Пол:7 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 tracker-extract amd64 2.3.3-2ubuntu0.20.04.1 [279 kB]
Пол:8 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 libgstreamer-plugins-bad1.0-0 amd64 1.16.3-0ubuntu1 [325 kB]
Получено 127 MB за 1мин 2с (2 032 kB/s)
(Чтение базы данных … на данный момент установлено 161615 файлов и каталогов.)
Подготовка к распаковке …/0-netplan.io_0.104-0ubuntu2~20.04.2_amd64.deb …
Распаковывается netplan.io (0.104-0ubuntu2~20.04.2) на замену (0.104-0ubuntu2~20.04.1) …
Подготовка к распаковке …/1-libnetplan0_0.104-0ubuntu2~20.04.2_amd64.deb …
Распаковывается libnetplan0:amd64 (0.104-0ubuntu2~20.04.2) на замену (0.104-0ubuntu2~20.04.1) …
Подготовка к распаковке …/2-libsnmp-base_5.8+dfsg-2ubuntu2.5_all.deb …
Распаковывается libsnmp-base (5.8+dfsg-2ubuntu2.5) на замену (5.8+dfsg-2ubuntu2.4) …
Подготовка к распаковке …/3-libsnmp35_5.8+dfsg-2ubuntu2.5_amd64.deb …
Распаковывается libsnmp35:amd64 (5.8+dfsg-2ubuntu2.5) на замену (5.8+dfsg-2ubuntu2.4) …
Подготовка к распаковке …/4-linux-firmware_1.187.33_all.deb …
Распаковывается linux-firmware (1.187.33) на замену (1.187.32) …
Подготовка к распаковке …/5-tracker-miner-fs_2.3.3-2ubuntu0.20.04.1_amd64.deb …
Распаковывается tracker-miner-fs (2.3.3-2ubuntu0.20.04.1) на замену (2.3.3-2) …
Подготовка к распаковке …/6-tracker-extract_2.3.3-2ubuntu0.20.04.1_amd64.deb …
Распаковывается tracker-extract (2.3.3-2ubuntu0.20.04.1) на замену (2.3.3-2) …
Подготовка к распаковке …/7-libgstreamer-plugins-bad1.0-0_1.16.3-0ubuntu1_amd64.deb …
Распаковывается libgstreamer-plugins-bad1.0-0:amd64 (1.16.3-0ubuntu1) на замену (1.16.2-2.1ubuntu1) …
Настраивается пакет tracker-extract (2.3.3-2ubuntu0.20.04.1) …
Настраивается пакет linux-firmware (1.187.33) …
update-initramfs: Generating /boot/initrd.img-5.15.0-46-generic
update-initramfs: Generating /boot/initrd.img-5.13.0-52-generic
Настраивается пакет libsnmp-base (5.8+dfsg-2ubuntu2.5) …
Настраивается пакет libnetplan0:amd64 (0.104-0ubuntu2~20.04.2) …
Настраивается пакет netplan.io (0.104-0ubuntu2~20.04.2) …
Настраивается пакет libgstreamer-plugins-bad1.0-0:amd64 (1.16.3-0ubuntu1) …
Настраивается пакет libsnmp35:amd64 (5.8+dfsg-2ubuntu2.5) …
Обрабатываются триггеры для dbus (1.12.16-2ubuntu2.2) …
Обрабатываются триггеры для libglib2.0-0:amd64 (2.64.6-1~ubuntu20.04.4) …
Обрабатываются триггеры для libc-bin (2.31-0ubuntu9.9) …
Обрабатываются триггеры для man-db (2.9.1-1) …
Настраивается пакет tracker-miner-fs (2.3.3-2ubuntu0.20.04.1) …
OK
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Сущ:3 http://security.ubuntu.com/ubuntu focal-security InRelease
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Пол:5 http://apt.postgresql.org/pub/repos/apt focal-pgdg InRelease [91,7 kB]
Пол:6 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 Packages [242 kB]
Получено 556 kB за 1с (421 kB/s)
Чтение списков пакетов… Готово
N: Пропускается получение настроенного файла «main/binary-i386/Packages», так как репозиторий «http://apt.postgresql.org/pub/repos/apt focal-pgdg InRelease» не поддерживает архитектуру «i386»
Чтение списков пакетов… Готово
Построение дерева зависимостей
Чтение информации о состоянии… Готово
Следующий пакет устанавливался автоматически и больше не требуется:
  libfwupdplugin1
Для его удаления используйте «sudo apt autoremove».
Будут установлены следующие дополнительные пакеты:
  libcommon-sense-perl libjson-perl libjson-xs-perl libllvm10 libpq5 libtypes-serialiser-perl pgdg-keyring
  postgresql-client-14 postgresql-client-common postgresql-common sysstat
Предлагаемые пакеты:
  postgresql-doc-14 isag
Следующие НОВЫЕ пакеты будут установлены:
  libcommon-sense-perl libjson-perl libjson-xs-perl libllvm10 libpq5 libtypes-serialiser-perl pgdg-keyring
  postgresql-14 postgresql-client-14 postgresql-client-common postgresql-common sysstat
Обновлено 0 пакетов, установлено 12 новых пакетов, для удаления отмечено 0 пакетов, и 0 пакетов не обновлено.
Необходимо скачать 33,9 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 136 MB.
Пол:1 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 libpq5 amd64 14.5-1.pgdg20.04+1 [173 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libcommon-sense-perl amd64 3.74-2build6 [20,1 kB]
Пол:3 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 pgdg-keyring all 2018.2 [10,7 kB]
Пол:4 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-client-common all 242.pgdg20.04+1 [92,2 kB]
Пол:5 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-client-14 amd64 14.5-1.pgdg20.04+1 [1 618 kB]
Пол:6 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libjson-perl all 4.02000-2 [80,9 kB]
Пол:7 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libtypes-serialiser-perl all 1.0-1 [12,1 kB]
Пол:8 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libjson-xs-perl amd64 4.020-1build1 [83,7 kB]
Пол:9 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libllvm10 amd64 1:10.0.0-4ubuntu1 [15,3 MB]
Пол:10 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-common all 242.pgdg20.04+1 [230 kB]
Пол:11 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-14 amd64 14.5-1.pgdg20.04+1 [15,8 MB]
Пол:12 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 sysstat amd64 12.2.0-2ubuntu0.1 [448 kB]
Получено 33,9 MB за 12с (2 885 kB/s)
Предварительная настройка пакетов …
Выбор ранее не выбранного пакета libcommon-sense-perl.
(Чтение базы данных … на данный момент установлено 161615 файлов и каталогов.)
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
Подготовка к распаковке …/05-libpq5_14.5-1.pgdg20.04+1_amd64.deb …
Распаковывается libpq5:amd64 (14.5-1.pgdg20.04+1) …
Выбор ранее не выбранного пакета pgdg-keyring.
Подготовка к распаковке …/06-pgdg-keyring_2018.2_all.deb …
Распаковывается pgdg-keyring (2018.2) …
Выбор ранее не выбранного пакета postgresql-client-common.
Подготовка к распаковке …/07-postgresql-client-common_242.pgdg20.04+1_all.deb …
Распаковывается postgresql-client-common (242.pgdg20.04+1) …
Выбор ранее не выбранного пакета postgresql-client-14.
Подготовка к распаковке …/08-postgresql-client-14_14.5-1.pgdg20.04+1_amd64.deb …
Распаковывается postgresql-client-14 (14.5-1.pgdg20.04+1) …
Выбор ранее не выбранного пакета postgresql-common.
Подготовка к распаковке …/09-postgresql-common_242.pgdg20.04+1_all.deb …
Добавляется «отклонение /usr/bin/pg_config в /usr/bin/pg_config.libpq-dev из-за postgresql-common»
Распаковывается postgresql-common (242.pgdg20.04+1) …
Выбор ранее не выбранного пакета postgresql-14.
Подготовка к распаковке …/10-postgresql-14_14.5-1.pgdg20.04+1_amd64.deb …
Распаковывается postgresql-14 (14.5-1.pgdg20.04+1) …
Выбор ранее не выбранного пакета sysstat.
Подготовка к распаковке …/11-sysstat_12.2.0-2ubuntu0.1_amd64.deb …
Распаковывается sysstat (12.2.0-2ubuntu0.1) …
Настраивается пакет pgdg-keyring (2018.2) …
Removing apt.postgresql.org key from trusted.gpg: OK
Настраивается пакет libpq5:amd64 (14.5-1.pgdg20.04+1) …
Настраивается пакет libcommon-sense-perl (3.74-2build6) …
Настраивается пакет libllvm10:amd64 (1:10.0.0-4ubuntu1) …
Настраивается пакет libtypes-serialiser-perl (1.0-1) …
Настраивается пакет libjson-perl (4.02000-2) …
Настраивается пакет sysstat (12.2.0-2ubuntu0.1) …

Creating config file /etc/default/sysstat with new version
update-alternatives: используется /usr/bin/sar.sysstat для предоставления /usr/bin/sar (sar) в автоматическом режиме
Created symlink /etc/systemd/system/multi-user.target.wants/sysstat.service → /lib/systemd/system/sysstat.service.
Настраивается пакет postgresql-client-common (242.pgdg20.04+1) …
Настраивается пакет libjson-xs-perl (4.020-1build1) …
Настраивается пакет postgresql-client-14 (14.5-1.pgdg20.04+1) …
update-alternatives: используется /usr/share/postgresql/14/man/man1/psql.1.gz для предоставления /usr/share/man/man1/psql.1.gz (psql.1.gz) в автоматическом режиме
Настраивается пакет postgresql-common (242.pgdg20.04+1) …
Добавление пользователя postgres в группу ssl-cert

Creating config file /etc/postgresql-common/createcluster.conf with new version
Building PostgreSQL dictionaries from installed myspell/hunspell packages...
  en_us
Removing obsolete dictionary files:
Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /lib/systemd/system/postgresql.service.
Настраивается пакет postgresql-14 (14.5-1.pgdg20.04+1) …
Creating new PostgreSQL cluster 14/main ...
/usr/lib/postgresql/14/bin/initdb -D /var/lib/postgresql/14/main --auth-local peer --auth-host scram-sha-256 --no-instructions
Файлы, относящиеся к этой СУБД, будут принадлежать пользователю "postgres".
От его имени также будет запускаться процесс сервера.

Кластер баз данных будет инициализирован с локалью "ru_RU.UTF-8".
Кодировка БД по умолчанию, выбранная в соответствии с настройками: "UTF8".
Выбрана конфигурация текстового поиска по умолчанию "russian".

Контроль целостности страниц данных отключён.

исправление прав для существующего каталога /var/lib/postgresql/14/main... ок
создание подкаталогов... ок
выбирается реализация динамической разделяемой памяти... posix
выбирается значение max_connections по умолчанию... 100
выбирается значение shared_buffers по умолчанию... 128MB
выбирается часовой пояс по умолчанию... Asia/Omsk
создание конфигурационных файлов... ок
выполняется подготовительный скрипт... ок
выполняется заключительная инициализация... ок
сохранение данных на диске... ок
update-alternatives: используется /usr/share/postgresql/14/man/man1/postmaster.1.gz для предоставления /usr/share/man/man1/postmaster.1.gz (postmaster.1.gz) в автоматическом режиме
Обрабатываются триггеры для systemd (245.4-4ubuntu3.17) …
Обрабатываются триггеры для man-db (2.9.1-1) …
Обрабатываются триггеры для libc-bin (2.31-0ubuntu9.9) …
root@user-virtual-machine:~#
```

```
curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.deb.sh | sudo bash
sudo apt -y install sysbench

sudo -u postgres psql -c "CREATE ROLE sbtest LOGIN SUPERUSER PASSWORD 'sbtest'"
sudo -u postgres psql -c "CREATE DATABASE sbtest"
sudo -u postgres sysbench \
--db-driver=pgsql \
--oltp-table-size=1000000 \
--oltp-tables-count=100 \
--threads=1 \
--pgsql-host=localhost \
--pgsql-port=5432 \
--pgsql-user=sbtest \
--pgsql-password=sbtest \
--pgsql-db=sbtest \
/usr/share/sysbench/tests/include/oltp_legacy/parallel_prepare.lua \
run

sudo -u postgres psql sbtest -c "select count(*) as tables, sum(n_live_tup) as rows, pg_size_pretty(pg_database_size('sbtest')) as size from pg_stat_user_tables"
```

таблиц | cтрок	   | размер
------ | --------- | ----------
100    | 100000000 | 24 Гб

### Делаем тест для каждого типа настроек

```
sysbench \
--db-driver=pgsql \
--report-interval=5 \
--oltp-table-size=1000000 \
--oltp-tables-count=100 \
--threads=64 \
--time=600 \
--pgsql-host=localhost \
--pgsql-port=5432 \
--pgsql-user=sbtest \
--pgsql-password=sbtest \
--pgsql-db=sbtest \
/usr/share/sysbench/tests/include/oltp_legacy/oltp.lua \
run 2>&1 | tee web.txt
```

### Результат HDD

```
SQL statistics:
    queries performed:
        read:                            4865126
        write:                           1389986
        other:                           695048
        total:                           6950160
    transactions:                        347499 (579.02 per sec.)
    queries:                             6950160 (11580.68 per sec.)
    ignored errors:                      10     (0.02 per sec.)
    reconnects:                          0      (0.00 per sec.)
General statistics:
total time:                          600.1494s
total number of events:              347499


Latency (ms):
min:                                    7.05
avg:                                  110.52
max:                                 1216.23
95th percentile:                      240.02
sum:                             38404223.34


Threads fairness:
events (avg/stddev):           5429.6719/25.35
execution time (avg/stddev):   600.0660/0.05
```

### Результат Веб - приложение 

Настройки
```
# DB Version: 14
# OS Type: linux
# DB Type: web
# Total Memory (RAM): 32 GB
# CPUs num: 8
# Connections num: 64
# Data Storage: ssd
max_connections = 64
shared_buffers = 8GB
effective_cache_size = 24GB
maintenance_work_mem = 2GB
checkpoint_completion_target = 0.9
wal_buffers = 16MB
default_statistics_target = 100
random_page_cost = 1.1
effective_io_concurrency = 200
work_mem = 32MB
min_wal_size = 1GB
max_wal_size = 4GB
max_worker_processes = 8
max_parallel_workers_per_gather = 4
max_parallel_workers = 8
max_parallel_maintenance_workers = 4
```

```
SQL statistics:
    queries performed:
        read:                            8897616
        write:                           2542122
        other:                           1271124
        total:                           12710862
    transactions:                        635535 (1059.03 per sec.)
    queries:                             12710862 (21180.83 per sec.)
    ignored errors:                      9      (0.01 per sec.)
    reconnects:                          0      (0.00 per sec.)
General statistics:
total time:                          600.1097s
total number of events:              635535


Latency (ms):
min:                                    5.77
avg:                                   60.42
max:                                  401.58
95th percentile:                      121.08
sum:                             38400941.40


Threads fairness:
events (avg/stddev):           9930.2344/46.32
execution time (avg/stddev):   600.0147/0.03
```

### Результат OLTP

```
# DB Version: 14
# OS Type: linux
# DB Type: oltp
# Total Memory (RAM): 32 GB
# CPUs num: 8
# Connections num: 100
# Data Storage: ssd
max_connections = 100
shared_buffers = 8GB
effective_cache_size = 24GB
maintenance_work_mem = 2GB
checkpoint_completion_target = 0.9
wal_buffers = 16MB
default_statistics_target = 100
random_page_cost = 1.1
effective_io_concurrency = 200
work_mem = 20971kB
min_wal_size = 2GB
max_wal_size = 8GB
max_worker_processes = 8
max_parallel_workers_per_gather = 4
max_parallel_workers = 8
max_parallel_maintenance_workers = 4
```

```
SQL statistics:
    queries performed:
        read:                            10673712
        write:                           3049599
        other:                           1524827
        total:                           15248138
    transactions:                        762397 (1270.43 per sec.)
    queries:                             15248138 (25408.94 per sec.)
    ignored errors:                      11     (0.02 per sec.)
    reconnects:                          0      (0.00 per sec.)
General statistics:
total time:                          600.1071s
total number of events:              762397


Latency (ms):
min:                                    5.50
avg:                                   50.37
max:                                  428.74
95th percentile:                       80.03
sum:                             38400023.08


Threads fairness:
events (avg/stddev):           11912.4531/50.89
execution time (avg/stddev):   600.0004/0.03
```

При работе теста видны просадки в tps как в случае с прошлым тестом, причина увеличение wal size
результат еще лучше чем в предыдущий 1059 против 1270 tps

### Результат Веб-приложение

```
# DB Version: 14
# OS Type: linux
# DB Type: oltp
# Total Memory (RAM): 32 GB
# CPUs num: 8
# Connections num: 100
# Data Storage: ssd
max_connections = 100
shared_buffers = 8GB
effective_cache_size = 24GB
work_mem = 328MB
maintenance_work_mem = 2GB
min_wal_size = 512MB
max_wal_size = 2GB
checkpoint_completion_target = 0.7
wal_buffers = 16MB
max_connections = 100
random_page_cost = 1.1
effective_io_concurrency = 200
max_worker_processes = 8
max_parallel_workers_per_gather = 4
max_parallel_workers = 8
```

```
SQL statistics:
    queries performed:
        read:                            6314112
        write:                           1803988
        other:                           902040
        total:                           9020140
    transactions:                        450998 (751.55 per sec.)
    queries:                             9020140 (15031.28 per sec.)
    ignored errors:                      10     (0.02 per sec.)
    reconnects:                          0      (0.00 per sec.)
General statistics:
total time:                          600.0895s
total number of events:              450998


Latency (ms):
min:                                    7.05
avg:                                   85.15
max:                                  487.11
95th percentile:                      139.85
sum:                             38401788.42


Threads fairness:
events (avg/stddev):           7046.8438/21.24
execution time (avg/stddev):   600.0279/0.02
```

В результате видно что после тестирования результат стал хуже
Наибольшим ключевым фактором по параметрам играет wal size
Для проверки будет проведен еще один тест


### Проверочный тест

```
# DB Version: 14
# OS Type: linux
# DB Type: oltp
# Total Memory (RAM): 32 GB
# CPUs num: 8
# Connections num: 100
# Data Storage: ssd
max_connections = 100
shared_buffers = 8GB
effective_cache_size = 24GB
maintenance_work_mem = 2GB
checkpoint_completion_target = 0.9
wal_buffers = 16MB
default_statistics_target = 100
random_page_cost = 1.1
effective_io_concurrency = 200
work_mem = 256MB
min_wal_size = 2GB
max_wal_size = 8GB
max_worker_processes = 8
max_parallel_workers_per_gather = 4
max_parallel_workers = 8
max_parallel_maintenance_workers = 4
```

```
SQL statistics:
    queries performed:
        read:                            9828700
        write:                           2808179
        other:                           1404117
        total:                           14040996
    transactions:                        702048 (1169.79 per sec.)
    queries:                             14040996 (23395.88 per sec.)
    ignored errors:                      2      (0.00 per sec.)
    reconnects:                          0      (0.00 per sec.)
General statistics:
total time:                          600.1463s
total number of events:              702048


Latency (ms):
min:                                    6.12
avg:                                   54.70
max:                                  334.50
95th percentile:                       92.42
sum:                             38399754.62


Threads fairness:
events (avg/stddev):           10969.5000/45.31
execution time (avg/stddev):   599.9962/0.04
```

Результат стал хуже


