# Репликация 

## реализовать горячее реплицирование для высокой доступности на 4ВМ. Источником должна выступать ВМ №3. Написать с какими проблемами столкнулись.

Выполняем на всех 3-х машинах кластера

```
echo "listen_addresses = '*'" | sudo tee -a /etc/postgresql/14/main/postgresql.conf
echo "wal_level = 'logical'" | sudo tee -a /etc/postgresql/14/main/postgresql.conf
echo "host all all 0.0.0.0/0 md5" | sudo tee -a /etc/postgresql/14/main/pg_hba.conf
echo "host replication all 0.0.0.0/0 md5" | sudo tee -a /etc/postgresql/14/main/pg_hba.conf

sudo systemctl restart postgresql

sudo -u postgres psql -c "CREATE USER demo SUPERUSER encrypted PASSWORD '1'"
```

### На 1 ВМ создаем таблицы test для записи, test2 для запросов на чтение.

```
sudo -u postgres psql -c "CREATE DATABASE demo"
sudo -u postgres psql demo -c "CREATE TABLE test1 (m text)"
sudo -u postgres psql demo -c "CREATE TABLE test2 (m text)"
```

### Создаем публикацию таблицы test и подписываемся на публикацию таблицы test2 с ВМ №2.

### 1 ВМ

```
sudo -u postgres psql demo -c "CREATE PUBLICATION test1_pub FOR TABLE test1"
```

### На 2 ВМ.

```
sudo -u postgres psql demo -c "CREATE SUBSCRIPTION test_sub CONNECTION 'host=hw9a port=5432 user=demo password=1 dbname=demo' PUBLICATION test1_pub WITH (copy_data = true)"
```

## На 2 ВМ создаем таблицы test2 для записи, test для запросов на чтение. Создаем публикацию таблицы test2 и подписываемся на публикацию таблицы test1 с ВМ №1

###  ВМ 2

```
sudo -u postgres psql demo -c "CREATE PUBLICATION test2_pub FOR TABLE test2"
```

### ВМ 1

```
sudo -u postgres psql demo -c "CREATE SUBSCRIPTION test2_sub CONNECTION 'host=hw9b port=5432 user=demo password=1 dbname=demo' PUBLICATION test2_pub WITH (copy_data = true)"
```

## Описание 

### 1 ВМ

```
sudo -u postgres psql demo -c "INSERT INTO test1 VALUES ('test')"
```

### 2 ВМ

```
sudo -u postgres psql demo -c "INSERT INTO test2 VALUES ('test2')"
```

### ВМ1

```
sudo -u postgres psql demo -c "select * from test2"
```

### 2 ВМ

```
sudo -u postgres psql demo -c "select * from test1"
```


```
sudo -u postgres psql demo -c "CREATE SUBSCRIPTION test_3 CONNECTION 'host=vm1 port=5432 user=demo password=1 dbname=demo' PUBLICATION test1_pub WITH (copy_data = true)"

sudo -u postgres psql demo -c "CREATE SUBSCRIPTION test_2 CONNECTION 'host=vm2 port=5432 user=demo password=1 dbname=demo' PUBLICATION test2_pub WITH (copy_data = true)"
```

Результат: 

ВМ1.test1 - ВМ2.test1
ВМ2.test2 - ВМ1.test2

Репликация

ВМ1.test1 - ВМ3.test1 
ВМ1.test2 - ВМ3.test2





