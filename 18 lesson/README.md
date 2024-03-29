# Сбор и использование статистики 

# Часть 1

## Создать индекс к какой-либо из таблиц вашей БД

```
create index idx_test_id on test(id);
```

## Прислать текстом результат команды explain, в которой используется данный индекс

```
Seq Scan on test  (cost=0.00..882.00 rows=50000 width=31)

```

## Реализовать индекс для полнотекстового поиска

```
update test
set is_okay = to_tsvector(is_okay);
```

## Реализовать индекс на часть таблицы или индекс на поле с функцией

```
postgres.public> create index idx_test_id_is_okay on test(lower(is_okay))
[2022-10-28 10:38:42] completed in 50 ms
```

## Создать индекс на несколько полей

```
postgres.public> CREATE INDEX idx_test_id_is_okay2 on test(id, is_okay)
[2022-10-28 10:38:48] completed in 23 ms

```

## Написать комментарии к каждому из индексов

```
postgres.public> COMMENT ON INDEX idx_test_id  is 'Индекс по колонке id'
[2022-10-28 10:43:13] completed in 3 ms
postgres.public> COMMENT ON INDEX idx_test_id_is_okay is 'Индекс на функцию'
[2022-10-28 10:43:13] completed in 1 ms
postgres.public> COMMENT ON INDEX idx_test_id_is_okay2  is 'Индекс на несколько полей'
[2022-10-28 10:43:13] completed in 2 ms
```

## Описать что и как делали и с какими проблемами столкнулись

Опираясь на 16 урок, все задания легко дались, единственный момент чтобы создать комментарии к индексам, пришлось почитать статью https://postgrespro.ru/docs/postgresql/9.6/sql-comment


# Часть 2

##  Реализовать прямое соединение двух или более таблиц

```
select * from bus b join model_bus mb on b.id_model=mb.id;

1,Москва-Болшево,1,1,1,ПАЗ
1,Москва-Болшево,1,1,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ
5,Москва-Волгорад,3,5,3,MAN
5,Москва-Волгорад,3,5,3,MAN

```

## Реализовать левостороннее (или правостороннее) соединение двух или более таблиц

```
select * from bus b left join model_bus mb on b.id_model=mb.id;

1,Москва-Болшево,1,1,1,ПАЗ
1,Москва-Болшево,1,1,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ
5,Москва-Волгорад,3,5,3,MAN
5,Москва-Волгорад,3,5,3,MAN
6,Москва-Иваново,,,,

```

## Реализовать кросс соединение двух или более таблиц

```
1,Москва-Болшево,1,1,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ
3,Москва-Ярославль,2,3,1,ПАЗ
4,Москва-Кострома,2,4,1,ПАЗ
5,Москва-Волгорад,3,5,1,ПАЗ
6,Москва-Иваново,,,1,ПАЗ
1,Москва-Болшево,1,1,2,ЛИАЗ
2,Москва-Пушкино,1,2,2,ЛИАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ
5,Москва-Волгорад,3,5,2,ЛИАЗ
6,Москва-Иваново,,,2,ЛИАЗ
1,Москва-Болшево,1,1,3,MAN
2,Москва-Пушкино,1,2,3,MAN
3,Москва-Ярославль,2,3,3,MAN
4,Москва-Кострома,2,4,3,MAN
5,Москва-Волгорад,3,5,3,MAN
6,Москва-Иваново,,,3,MAN
1,Москва-Болшево,1,1,4,МАЗ
2,Москва-Пушкино,1,2,4,МАЗ
3,Москва-Ярославль,2,3,4,МАЗ
4,Москва-Кострома,2,4,4,МАЗ
5,Москва-Волгорад,3,5,4,МАЗ
6,Москва-Иваново,,,4,МАЗ
1,Москва-Болшево,1,1,5,НЕФАЗ
2,Москва-Пушкино,1,2,5,НЕФАЗ
3,Москва-Ярославль,2,3,5,НЕФАЗ
4,Москва-Кострома,2,4,5,НЕФАЗ
5,Москва-Волгорад,3,5,5,НЕФАЗ
6,Москва-Иваново,,,5,НЕФАЗ
1,Москва-Болшево,1,1,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ
3,Москва-Ярославль,2,3,1,ПАЗ
4,Москва-Кострома,2,4,1,ПАЗ
5,Москва-Волгорад,3,5,1,ПАЗ
6,Москва-Иваново,,,1,ПАЗ
1,Москва-Болшево,1,1,2,ЛИАЗ
2,Москва-Пушкино,1,2,2,ЛИАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ
5,Москва-Волгорад,3,5,2,ЛИАЗ
6,Москва-Иваново,,,2,ЛИАЗ
1,Москва-Болшево,1,1,3,MAN
2,Москва-Пушкино,1,2,3,MAN
3,Москва-Ярославль,2,3,3,MAN
4,Москва-Кострома,2,4,3,MAN
5,Москва-Волгорад,3,5,3,MAN
6,Москва-Иваново,,,3,MAN
1,Москва-Болшево,1,1,4,МАЗ
2,Москва-Пушкино,1,2,4,МАЗ
3,Москва-Ярославль,2,3,4,МАЗ
4,Москва-Кострома,2,4,4,МАЗ
5,Москва-Волгорад,3,5,4,МАЗ
6,Москва-Иваново,,,4,МАЗ
1,Москва-Болшево,1,1,5,НЕФАЗ
2,Москва-Пушкино,1,2,5,НЕФАЗ
3,Москва-Ярославль,2,3,5,НЕФАЗ
4,Москва-Кострома,2,4,5,НЕФАЗ
5,Москва-Волгорад,3,5,5,НЕФАЗ
6,Москва-Иваново,,,5,НЕФАЗ

```

## Реализовать полное соединение двух или более таблиц

```
select * from bus b full join model_bus mb on b.id_model=mb.id;

1,Москва-Болшево,1,1,1,ПАЗ
1,Москва-Болшево,1,1,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ
5,Москва-Волгорад,3,5,3,MAN
5,Москва-Волгорад,3,5,3,MAN
6,Москва-Иваново,,,,
,,,,4,МАЗ
,,,,4,МАЗ
,,,,5,НЕФАЗ
,,,,5,НЕФАЗ

```

##  Реализовать запрос, в котором будут использованы разные типы соединений

```
select * from bus b right join model_bus mb on b.id_model=mb.id
    left join model_bus mb2 on b.id_model=mb2.id;

1,Москва-Болшево,1,1,1,ПАЗ,1,ПАЗ
1,Москва-Болшево,1,1,1,ПАЗ,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ,1,ПАЗ
1,Москва-Болшево,1,1,1,ПАЗ,1,ПАЗ
1,Москва-Болшево,1,1,1,ПАЗ,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ,1,ПАЗ
2,Москва-Пушкино,1,2,1,ПАЗ,1,ПАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ,2,ЛИАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ,2,ЛИАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ,2,ЛИАЗ
3,Москва-Ярославль,2,3,2,ЛИАЗ,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ,2,ЛИАЗ
4,Москва-Кострома,2,4,2,ЛИАЗ,2,ЛИАЗ
5,Москва-Волгорад,3,5,3,MAN,3,MAN
5,Москва-Волгорад,3,5,3,MAN,3,MAN
5,Москва-Волгорад,3,5,3,MAN,3,MAN
5,Москва-Волгорад,3,5,3,MAN,3,MAN
,,,,4,МАЗ,,
,,,,4,МАЗ,,
,,,,5,НЕФАЗ,,
,,,,5,НЕФАЗ,,

```

## Сделать комментарии на каждый запрос

```
1. Получаем список всех автобусов и моделей к ним 
2. Получем список всех автобусов и моделей к ним включая отсутствующие модели.
3. Получаем все (перекрестные) варианты автобусов и моделей к ним.(Иногда именуется Декартово произведение)
4. Получаем список автобусов и моделей к ним, включая результаты когда есть автобус но нет модели и когда есть модель но нет автобуса.
5. Создаем левосторонее и правосторонее соединение таблиц. В результате получаем запрос в котором у нас есть дублирующие записи автобусов и моделей к ним с левой и правой таблиц + список с моделями но без автобусов.
```

## К работе приложить структуру таблиц, для которых выполнялись соединения

```
create table bus (id serial,route text,id_model int,id_driver int);
create table model_bus (id serial,name text);
create table driver (id serial,first_name text,second_name text);
insert into bus values (1,'Москва-Болшево',1,1),(2,'Москва-Пушкино',1,2),(3,'Москва-Ярославль',2,3),(4,'Москва-Кострома',2,4),(5,'Москва-Волгорад',3,5),(6,'Москва-Иваново',null,null);
insert into model_bus values(1,'ПАЗ'),(2,'ЛИАЗ'),(3,'MAN'),(4,'МАЗ'),(5,'НЕФАЗ');
insert into driver values(1,'Иван','Иванов'),(2,'Петр','Петров'),(3,'Савелий','Сидоров'),(4,'Антон','Шторкин'),(5,'Олег','Зажигаев'),(6,'Аркадий','Паровозов');

```
























