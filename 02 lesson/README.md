# Работа с уровнями изоляции транзакции в PostgreSQL
## Установка PostgreSQL
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20%D0%9F%D0%BE%D1%81%D0%B3%D1%80%D0%B51.png?raw=true)
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20%D0%9F%D0%BE%D1%81%D0%B3%D1%80%D0%B52.png?raw=true)
## Вход по второй сессии ssh
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%92%D0%BE%D0%B9%D1%82%D0%B8%20%D0%B2%D1%82%D0%BE%D1%80%D0%B0%D1%8F%20%D1%81%D1%81%D0%B5%D1%81%D0%B8%D1%8F%20ssh.png?raw=true)
## Запустить везде psql из под пользователя postgres
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D1%8C%20%D0%B2%D0%B5%D0%B7%D0%B4%D0%B5%20%D0%BF%D0%BE%D1%81%D1%82%D0%B3%D1%80%D0%B5%D1%812.png?raw=true)
## Выключить auto commit
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%B2%D1%8B%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C%20auto%20commit.png?raw=true)
## Cделать в первой сессии новую таблицу и наполнить ее данными
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/C%D0%B4%D0%B5%D0%BB%D0%B0%D1%82%D1%8C%20%D0%B2%20%D0%BF%D0%B5%D1%80%D0%B2%D0%BE%D0%B9%20%D1%81%D0%B5%D1%81%D1%81%D0%B8%D0%B8%20%D0%BD%D0%BE%D0%B2%D1%83%D1%8E%20%D1%82%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D1%83%20%D0%B8%20%D0%BD%D0%B0%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D1%8C%20%D0%B5%D0%B5%20%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8.png?raw=true)
## Посмотреть текущий уровень изоляции
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%9F%D0%BE%D1%81%D0%BC%D0%BE%D1%82%D1%80%D0%B5%D1%82%D1%8C%20%D1%82%D0%B5%D0%BA%D1%83%D1%89%D0%B8%D0%B9%20%D1%83%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C%20%D0%B8%D0%B7%D0%BE%D0%BB%D1%8F%D1%86%D0%B8%D0%B8.png?raw=true)
## В первой сессии добавить новую запись 
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%B2%20%D0%BF%D0%B5%D1%80%D0%B2%D0%BE%D0%B9%20%D1%81%D0%B5%D1%81%D1%81%D0%B8%D0%B8%20%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%B8%D1%82%D1%8C%20%D0%BD%D0%BE%D0%B2%D1%83%D1%8E%20%D0%B7%D0%B0%D0%BF%D0%B8%D1%81%D1%8C%20.png?raw=true)
## сделать select * from persons во второй сессии
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D1%81%D0%B4%D0%B5%D0%BB%D0%B0%D1%82%D1%8C%20select%20all%20from%20persons%20%D0%B2%D0%BE%20%D0%B2%D1%82%D0%BE%D1%80%D0%BE%D0%B9%20%D1%81%D0%B5%D1%81%D1%81%D0%B8%D0%B8.png?raw=true)
## видите ли вы новую запись и если да то почему?
Новую запись во второй сессии не видно потому что включена опция \set AUTOCOMMIT OFF в первой сессии, внесена новая запись но небыло команды commit(подтверждение внесения данных в таблицу persons) в первой сессии.
## завершить первую транзакцию - commit; сделать select * from persons во второй сессии
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%B7%D0%B0%D0%B2%D0%B5%D1%80%D1%88%D0%B8%D1%82%D1%8C%20%D0%BF%D0%B5%D1%80%D0%B2%D1%83%D1%8E%20%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D1%8E%20-%20commit;.png?raw=true)
## видите ли вы новую запись и если да то почему?
Новую запись видно, потому что в первой сессии после применения операции commit было произведено подтверждение всех внесенных изменений(подтверждение транзакции).
## начать новые но уже repeatable read транзации
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%BD%D0%B0%D1%87%D0%B0%D1%82%D1%8C%20%D0%BD%D0%BE%D0%B2%D1%8B%D0%B5%20%D0%BD%D0%BE%20%D1%83%D0%B6%D0%B5%20repeatable%20read%20%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D1%86%D0%B8%D0%B8.png?raw=true)
## в первой сессии добавить новую запись insert into persons(first_name, second_name) values('sveta', 'svetova'); сделать select * from persons во второй сессии
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%B2%20%D0%BF%D0%B5%D1%80%D0%B2%D0%BE%D0%B9%20%D1%81%D0%B5%D1%81%D1%81%D0%B8%D0%B8%20%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%B8%D1%82%D1%8C%20%D0%BD%D0%BE%D0%B2%D1%83%D1%8E%20%D0%B7%D0%B0%D0%BF%D0%B8%D1%81%D1%8C2.png?raw=true)
Запись не видно во второй сессии т.к. включен режим repeatable read и опция \set AUTOCOMMIT OFF
## завершить первую транзакцию - commit; сделать select * from persons во второй сессии
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/Screenshot%202022-07-12%20121626.png?raw=true)
## видите ли вы новую запись и если да то почему?
Запись не видно во второй сессии т.к. включен режим repeatable read и опция \set AUTOCOMMIT OFF и во второй сессии не подтверждена транзакция на select (через commit).
## завершить вторую транзакцию и сделать select * from persons во второй сессии
![Image alt](https://github.com/Sistem-Pack/otus/blob/main/02%20lesson/%D0%B7%D0%B0%D0%B2%D0%B5%D1%80%D1%88%D0%B8%D1%82%D1%8C%20%D0%B2%D1%82%D0%BE%D1%80%D1%83%D1%8E%20%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D1%8E3.png?raw=true)
Запись видно, потому что во второй сессии подтверждена транзакция на выборку данных из таблицы select посредством операции commit.
