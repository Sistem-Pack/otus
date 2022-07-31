# Физический уровень PostgreSQL
## поставьте на нее PostgreSQL 14 через sudo apt
```
root@user-virtual-machine:~# sudo apt update && sudo apt upgrade -y -q && sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo apt -y install postgresql-14
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://security.ubuntu.com/ubuntu focal-security InRelease
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Получено 222 kB за 1с (251 kB/s)
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
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Сущ:3 http://security.ubuntu.com/ubuntu focal-security InRelease
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Пол:5 http://apt.postgresql.org/pub/repos/apt focal-pgdg InRelease [91,7 kB]
Пол:6 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 Packages [240 kB]
Получено 554 kB за 1с (412 kB/s)
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
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libcommon-sense-perl amd64 3.74-2build6 [20,1 kB]
Пол:2 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 libpq5 amd64 14.4-1.pgdg20.04+1 [172 kB]
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libjson-perl all 4.02000-2 [80,9 kB]
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libtypes-serialiser-perl all 1.0-1 [12,1 kB]
Пол:5 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libjson-xs-perl amd64 4.020-1build1 [83,7 kB]
Пол:6 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libllvm10 amd64 1:10.0.0-4ubuntu1 [15,3 MB]
Пол:7 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 pgdg-keyring all 2018.2 [10,7 kB]
Пол:8 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-client-common all 241.pgdg20.04+1 [92,1 kB]
Пол:9 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-client-14 amd64 14.4-1.pgdg20.04+1 [1 623 kB]
Пол:10 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-common all 241.pgdg20.04+1 [230 kB]
Пол:11 http://apt.postgresql.org/pub/repos/apt focal-pgdg/main amd64 postgresql-14 amd64 14.4-1.pgdg20.04+1 [15,8 MB]
Пол:12 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 sysstat amd64 12.2.0-2ubuntu0.1 [448 kB]
Получено 33,9 MB за 11с (3 119 kB/s)
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
Выбор ранее не выбранного пакета postgresql-client-14.
Подготовка к распаковке …/08-postgresql-client-14_14.4-1.pgdg20.04+1_amd64.deb …
Распаковывается postgresql-client-14 (14.4-1.pgdg20.04+1) …
Выбор ранее не выбранного пакета postgresql-common.
Подготовка к распаковке …/09-postgresql-common_241.pgdg20.04+1_all.deb …
Добавляется «отклонение /usr/bin/pg_config в /usr/bin/pg_config.libpq-dev из-за postgresql-common»
Распаковывается postgresql-common (241.pgdg20.04+1) …
Выбор ранее не выбранного пакета postgresql-14.
Подготовка к распаковке …/10-postgresql-14_14.4-1.pgdg20.04+1_amd64.deb …
Распаковывается postgresql-14 (14.4-1.pgdg20.04+1) …
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
Настраивается пакет postgresql-client-14 (14.4-1.pgdg20.04+1) …
update-alternatives: используется /usr/share/postgresql/14/man/man1/psql.1.gz для предоставления /usr/share/man/man1/psql.1.gz (psql.1.gz) в автоматическом режиме
Настраивается пакет postgresql-common (241.pgdg20.04+1) …
Добавление пользователя postgres в группу ssl-cert

Creating config file /etc/postgresql-common/createcluster.conf with new version
Building PostgreSQL dictionaries from installed myspell/hunspell packages...
  en_us
Removing obsolete dictionary files:
Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /lib/systemd/system/postgresql.service.
Настраивается пакет postgresql-14 (14.4-1.pgdg20.04+1) …
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
```
## проверьте что кластер запущен через sudo -u postgres pg_lsclusters
```
root@user-virtual-machine:~# sudo -u postgres pg_lsclusters
Ver Cluster Port Status Owner    Data directory              Log file
14  main    5432 online postgres /var/lib/postgresql/14/main /var/log/postgresql/postgresql-14-main.log
root@user-virtual-machine:~#
```
## зайдите из под пользователя postgres в psql и сделайте произвольную таблицу с произвольным содержимым postgres=# create table test(c1 text); postgres=# insert into test values('1'); \q
```
sudo -u postgres psql -p 5433
postgres=# create table test(c1 text); insert into test values('1'); \q
INSERT 0 1
```
## остановите postgres например через sudo -u postgres pg_ctlcluster 14 main stop
```
root@user-virtual-machine:~# sudo -u postgres pg_ctlcluster 14 main stop
Cluster is not running.
```
## подключить диск
```
Подключен диск на 10 Gb через VMware Workstation
```
```
Диск /dev/sdb: 10 GiB, 10737418240 байт, 20971520 секторов
Disk model: VMware Virtual S
Единицы: секторов по 1 * 512 = 512 байт
Размер сектора (логический/физический): 512 байт / 512 байт
Размер I/O (минимальный/оптимальный): 512 байт / 512 байт
```

## Размечаем диск
```
root@user-virtual-machine:~# mkdir /mnt/data
root@user-virtual-machine:~# mkfs.ext4 -L postgresdata /dev/sdb
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 2621440 4k blocks and 655360 inodes
Filesystem UUID: 2721b736-a4ab-4b29-86ec-8d4e44d59fbc
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done
Сохранение таблицы inod'ов: done
Создание журнала (16384 блоков): готово
Writing superblocks and filesystem accounting information: готово
root@user-virtual-machine:~# mount -o defaults /dev/sdb /mnt/data
```
## сделайте пользователя postgres владельцем /mnt/data
```
root@user-virtual-machine:~# chown -R postgres:postgres /mnt/data/
```
## перенесите содержимое /var/lib/postgres/14 в /mnt/data
```
root@user-virtual-machine:~# mv /var/lib/postgresql/14 /mnt/data
```
## попытайтесь запустить кластер
```
root@user-virtual-machine:~# sudo -u postgres pg_ctlcluster 14 main start
Error: /var/lib/postgresql/14/main is not accessible or does not exist
```
## напишите получилось или нет и почему

```
Не получилось, так как нет данных в нужном месте и необходимо произвести настройку конфигурационного файла
```
