# Секционирование 

```
curl https://edu.postgrespro.ru/demo_small.zip
unzip demo_small.zip
docker run -it --rm -p 5432:5432 -v $PWD:/demo --name=db -e POSTGRES_PASSWORD=123 -e POSTGRES_DB=demo postgres:13-alpine
docker exec -it db psql -U postgres -f /demo/demo_small.sql
```

## Database Image

![Image alt](https://github.com/Sistem-Pack/otus/blob/main/20%20lesson/flights_base.svg)

```
-- Реализовать прямое соединение двух или более таблиц

-- top 5 городов
select a.aircraft_code, dep.city departure, arr.city arrive, count(*)
from bookings.aircrafts a
         join bookings.flights f on a.aircraft_code = f.aircraft_code
         join bookings.airports dep on dep.airport_code = f.departure_airport
         join bookings.airports arr on arr.airport_code = f.departure_airport
group by 1, 2, 3
order by 4 desc
limit 5

-- Реализовать левостороннее (или правостороннее) соединение двух или более таблиц

-- заполняемость при перелетах
select f.flight_id, count(tf.*) / count(s.*) * 100 from bookings.flights f
join bookings.aircrafts a on f.aircraft_code = a.aircraft_code
join bookings.seats s on a.aircraft_code = s.aircraft_code
left join bookings.ticket_flights tf on f.flight_id = tf.flight_id
group by 1

-- Реализовать кросс соединение двух или более таблиц
-- Реализовать полное соединение двух или более таблиц

-- самые дальние друг от друга аэропорты
select a.city, b.city, (point(a.longitude,a.latitude) <@> point(b.longitude,b.latitude)) as distance from bookings.airports a
cross join bookings.airports b
order by distance desc
limit 1
```

## Описание

### Самые быстрые меняемые таблички которые скорее всего потребуют отдельной настройки для autovacuum

```
select n_mod_since_analyze + n_ins_since_vacuum / EXTRACT(EPOCH FROM (now() - last_autovacuum)), relname from pg_stat_user_tables
where last_autovacuum is not null
order by 1 desc
```

### Возможные узкие места которые вызовут загрузку базы

```
select
EXTRACT(EPOCH FROM (now() - state_change)) as idle_seconds,
pid
from pg_stat_activity
where state = 'idle' and EXTRACT(EPOCH FROM (now() - state_change)) > 60
```

### Список загруженных баз

```
select
(tup_inserted + tup_deleted + tup_updated) / EXTRACT(EPOCH FROM (now() - stats_reset)) writes_per_second,
tup_returned / EXTRACT(EPOCH FROM (now() - stats_reset)) reads_per_second,
datname
from pg_stat_database
```