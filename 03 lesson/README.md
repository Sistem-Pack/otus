# Установка и настройка PostgreSQL в контейнере Docker
## Установка Docker Engine
Установка Docker Engine согласно оф. документации:
```
1. sudo apt-get remove docker docker-engine docker.io containerd runc
2. sudo apt-get update 
3. apt-get install \    ca-certificates \    curl \    gnupg \    lsb-release
4. sudo mkdir -p /etc/apt/keyrings
5. curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
6.echo \ "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
## сделать каталог /var/lib/postgres
```
mkdir /var/lib/postgres
```
## развернуть контейнер с PostgreSQL 14 смонтировав в него /var/lib/postgres

1. Подготовимся к следующим пунктам 
1.1. Создадим Докер-сеть:
```
	docker network create pg-net
	ea75b5d386df7da459d235d9c3251f4bff5f5e6266ffcf0727fc91ec2c649901
```
2. подключаем созданную сеть к контейнеру сервера Postgres:
```
sudo docker run --name pg --network pg-net -e POSTGRES_PASSWORD=1 -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres:14
Unable to find image 'postgres:14' locally
14: Pulling from library/postgres
461246efe0a7: Pull complete
8d6943e62c54: Pull complete
558c55f04e35: Pull complete
186be55594a7: Pull complete
f38240981157: Pull complete
e0699dc58a92: Pull complete
066f440c89a6: Pull complete
ce20e6e2a202: Pull complete
c0f13eb40c44: Pull complete
3d7e9b569f81: Pull complete
2ab91678d745: Pull complete
ffc80af02e8a: Pull complete
f3a57056b036: Pull complete
Digest: sha256:3e2eba0a6efbeb396e086c332c5a85be06997d2cf573d34794764625f405df4e
Status: Downloaded newer image for postgres:14
338db57784cfeb70860a45077b3f96e7b53f04dfbda95506d6d2dc3e35b630fd
```

## развернуть контейнер с клиентом postgres

```
docker run -it --rm --network pg-net --name pg-client postgres:14 psql -h pg -U postgres
Password for user postgres:
psql (14.4 (Debian 14.4-1.pgdg110+1))
Type "help" for help.

postgres=#
```

## подключится из контейнера с клиентом к контейнеру с сервером и сделать таблицу с парой строк

```
postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
(3 rows)

postgres=# SELECT current_database();
 current_database
------------------
 postgres
(1 row)

postgres=# CREATE TABLE test (i serial, amount int);
CREATE TABLE
postgres=# INSERT INTO test(amount) VALUES (100);
INSERT 0 1
postgres=# INSERT INTO test(amount) VALUES (500);
INSERT 0 1
postgres=# SELECT * FROM test;
 i | amount
---+--------
 1 |    100
 2 |    500
(2 rows)

postgres=#
```

## подключится к контейнеру с сервером с ноутбука/компьютера извне инстансов GCP/места установки докера

```
sudo psql -p 5432 -U postgres -h 192.168.218.135 -d postgres -W

Password for user postgres:
psql (14.4 (Debian 14.4-1.pgdg110+1))
Type "help" for help.

postgres=#
```

## удалить контейнер с сервером

```
root@user-virtual-machine:~# docker stop pg
pg
root@user-virtual-machine:~# docker rm pg
pg
```

## создать его заново

```
root@user-virtual-machine:~# sudo docker run --name pg --network pg-net -e POSTGRES_PASSWORD=1 -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres:14
d2470e492649a697d7b20d86789e3e7a0e63021106a6755c21ced2db83e33323
```

## подключится снова из контейнера с клиентом к контейнеру с сервером

```
docker run -it --rm --network pg-net --name pg-client postgres:14 psql -h pg -U postgres
Password for user postgres:
psql (14.4 (Debian 14.4-1.pgdg110+1))
Type "help" for help.

postgres=#

## проверить, что данные остались на месте

select * from test;
 i | amount
---+--------
 1 |    100
 2 |    500
(2 rows)
```