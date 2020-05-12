# MySQL_Data_Types

## DECIMAL
```
mysql> CREATE TABLE items(price DECIMAL(5,2));
Query OK, 0 rows affected (0.05 sec)

mysql> INSERT INTO items(price) VALUES(7);
Query OK, 1 row affected (0.01 sec)

mysql>
mysql> INSERT INTO items(price) VALUES(7987654);
Query OK, 1 row affected, 1 warning (0.05 sec)

mysql>
mysql> INSERT INTO items(price) VALUES(34.88);
Query OK, 1 row affected (0.01 sec)

mysql>
mysql> INSERT INTO items(price) VALUES(298.9999);
Query OK, 1 row affected, 1 warning (0.01 sec)

mysql>
mysql> INSERT INTO items(price) VALUES(1.9999);
Query OK, 1 row affected, 1 warning (0.01 sec)

mysql>
mysql> SELECT * FROM items;
+--------+
| price  |
+--------+
|   7.00 |
| 999.99 |
|  34.88 |
| 299.00 |
|   2.00 |
+--------+
5 rows in set (0.00 sec)
```
## FLOAT and DOUBLE
```
mysql> CREATE TABLE thingies (price FLOAT);
Query OK, 0 rows affected (0.05 sec)

mysql>
mysql> INSERT INTO thingies(price) VALUES (88.45);
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM thingies;
+-------+
| price |
+-------+
| 88.45 |
+-------+
1 row in set (0.00 sec)

mysql>
mysql> INSERT INTO thingies(price) VALUES (8877.45);
Query OK, 1 row affected (0.08 sec)

mysql>
mysql> SELECT * FROM thingies;
+---------+
| price   |
+---------+
|   88.45 |
| 8877.45 |
+---------+
2 rows in set (0.00 sec)

mysql>
mysql> INSERT INTO thingies(price) VALUES (8877665544.45);
Query OK, 1 row affected (0.02 sec)

mysql>
mysql> SELECT * FROM thingies;
+------------+
| price      |
+------------+
|      88.45 |
|    8877.45 |
| 8877670000 |
+------------+
3 rows in set (0.00 sec)

```

## DATE, TIME, DATETIME, CURDATE(), CURTIME(), NOW()
```
mysql> CREATE TABLE people (
    ->   name varchar(100),
    ->   birthdate date,
    ->   birthtime time,
    ->   birthdt datetime
    -> );
Query OK, 0 rows affected (0.07 sec)

mysql> INSERT INTO people (name, birthdate, birthtime, birthdt)
    ->   VALUES ('Padma', '1983-11-11', '10:07:35', '1983-11-11 10:07:35');
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO people (name, birthdate, birthtime, birthdt)
    -> VALUES('Larry', '1943-12-25', '04:10:42', '1943-12-25 04:10:42');
Query OK, 1 row affected (0.04 sec)

mysql>
mysql> SELECT * FROM people;
+-------+------------+-----------+---------------------+
| name  | birthdate  | birthtime | birthdt             |
+-------+------------+-----------+---------------------+
| Padma | 1983-11-11 | 10:07:35  | 1983-11-11 10:07:35 |
| Larry | 1943-12-25 | 04:10:42  | 1943-12-25 04:10:42 |
+-------+------------+-----------+---------------------+
2 rows in set (0.00 sec)

mysql> INSERT INTO people (name, birthdate, birthtime, birthdt) VALUES('LarryCur', CURDATE(), CURTIME(), NOW
());
Query OK, 1 row affected (0.05 sec)

mysql> SELECT * FROM people;
+----------+------------+-----------+---------------------+
| name     | birthdate  | birthtime | birthdt             |
+----------+------------+-----------+---------------------+
| Padma    | 1983-11-11 | 10:07:35  | 1983-11-11 10:07:35 |
| Larry    | 1943-12-25 | 04:10:42  | 1943-12-25 04:10:42 |
| LarryCur | 2020-05-12 | 18:26:14  | 2020-05-12 18:26:14 |
+----------+------------+-----------+---------------------+
3 rows in set (0.00 sec)
```

## Date and TIME Functions
[MySQL_DATETIME_Doc](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)
```
mysql> SELECT name, birthdate FROM people;
+----------+------------+
| name     | birthdate  |
+----------+------------+
| Padma    | 1983-11-11 |
| Larry    | 1943-12-25 |
| LarryCur | 2020-05-12 |
+----------+------------+
3 rows in set (0.18 sec)

mysql> SELECT name, birthdate, DAY(birthdate) FROM people;
+----------+------------+----------------+
| name     | birthdate  | DAY(birthdate) |
+----------+------------+----------------+
| Padma    | 1983-11-11 |             11 |
| Larry    | 1943-12-25 |             25 |
| LarryCur | 2020-05-12 |             12 |
+----------+------------+----------------+
3 rows in set (0.00 sec)
mysql> SELECT name, birthdate, DAYNAME(birthdate) FROM people;
+----------+------------+--------------------+
| name     | birthdate  | DAYNAME(birthdate) |
+----------+------------+--------------------+
| Padma    | 1983-11-11 | Friday             |
| Larry    | 1943-12-25 | Saturday           |
| LarryCur | 2020-05-12 | Tuesday            |
+----------+------------+--------------------+
3 rows in set (0.00 sec)

mysql> SELECT name, birthdate, DAYOFWEEK(birthdate) FROM people;
+----------+------------+----------------------+
| name     | birthdate  | DAYOFWEEK(birthdate) |
+----------+------------+----------------------+
| Padma    | 1983-11-11 |                    6 |
| Larry    | 1943-12-25 |                    7 |
| LarryCur | 2020-05-12 |                    3 |
+----------+------------+----------------------+
3 rows in set (0.00 sec)

mysql> SELECT name, birthdate, DAYOFYEAR(birthdate) FROM people;
+----------+------------+----------------------+
| name     | birthdate  | DAYOFYEAR(birthdate) |
+----------+------------+----------------------+
| Padma    | 1983-11-11 |                  315 |
| Larry    | 1943-12-25 |                  359 |
| LarryCur | 2020-05-12 |                  133 |
+----------+------------+----------------------+
3 rows in set (0.01 sec)

mysql> SELECT name, birthdt, DAYOFYEAR(birthdt) FROM people;
+----------+---------------------+--------------------+
| name     | birthdt             | DAYOFYEAR(birthdt) |
+----------+---------------------+--------------------+
| Padma    | 1983-11-11 10:07:35 |                315 |
| Larry    | 1943-12-25 04:10:42 |                359 |
| LarryCur | 2020-05-12 18:26:14 |                133 |
+----------+---------------------+--------------------+
3 rows in set (0.00 sec)

mysql> SELECT name, birthdt, MONTH(birthdt) FROM people;
+----------+---------------------+----------------+
| name     | birthdt             | MONTH(birthdt) |
+----------+---------------------+----------------+
| Padma    | 1983-11-11 10:07:35 |             11 |
| Larry    | 1943-12-25 04:10:42 |             12 |
| LarryCur | 2020-05-12 18:26:14 |              5 |
+----------+---------------------+----------------+
3 rows in set (0.00 sec)

mysql> SELECT name, birthdt, MONTHNAME(birthdt) FROM people;
+----------+---------------------+--------------------+
| name     | birthdt             | MONTHNAME(birthdt) |
+----------+---------------------+--------------------+
| Padma    | 1983-11-11 10:07:35 | November           |
| Larry    | 1943-12-25 04:10:42 | December           |
| LarryCur | 2020-05-12 18:26:14 | May                |
+----------+---------------------+--------------------+
3 rows in set (0.01 sec)

mysql> SELECT name, birthtime, HOUR(birthtime) FROM people;
+----------+-----------+-----------------+
| name     | birthtime | HOUR(birthtime) |
+----------+-----------+-----------------+
| Padma    | 10:07:35  |              10 |
| Larry    | 04:10:42  |               4 |
| LarryCur | 18:26:14  |              18 |
+----------+-----------+-----------------+
3 rows in set (0.00 sec)

mysql> SELECT
    ->   CONCAT(MONTHNAME(birthdate), ' ', DAY(birthdate), ' ', YEAR(birthdate))
    -> FROM people;
+-------------------------------------------------------------------------+
| CONCAT(MONTHNAME(birthdate), ' ', DAY(birthdate), ' ', YEAR(birthdate)) |
+-------------------------------------------------------------------------+
| November 11 1983                                                        |
| December 25 1943                                                        |
| May 12 2020                                                             |
+-------------------------------------------------------------------------+
3 rows in set (0.00 sec)

mysql> SELECT DATE_FORMAT(birthdt, 'Was born on a %W') FROM people;
+------------------------------------------+
| DATE_FORMAT(birthdt, 'Was born on a %W') |
+------------------------------------------+
| Was born on a Friday                     |
| Was born on a Saturday                   |
| Was born on a Tuesday                    |
+------------------------------------------+
3 rows in set (0.00 sec)

mysql> SELECT DATE_FORMAT(birthdt, '%m/%d/%Y') FROM people;
+----------------------------------+
| DATE_FORMAT(birthdt, '%m/%d/%Y') |
+----------------------------------+
| 11/11/1983                       |
| 12/25/1943                       |
| 05/12/2020                       |
+----------------------------------+
3 rows in set (0.00 sec)

mysql> SELECT DATE_FORMAT(birthdt, '%m/%d/%Y at %h:%i') FROM people;
+-------------------------------------------+
| DATE_FORMAT(birthdt, '%m/%d/%Y at %h:%i') |
+-------------------------------------------+
| 11/11/1983 at 10:07                       |
| 12/25/1943 at 04:10                       |
| 05/12/2020 at 06:26                       |
+-------------------------------------------+
3 rows in set (0.00 sec)
```

## Date Math
```
mysql> SELECT * FROM people;
+----------+------------+-----------+---------------------+
| name     | birthdate  | birthtime | birthdt             |
+----------+------------+-----------+---------------------+
| Padma    | 1983-11-11 | 10:07:35  | 1983-11-11 10:07:35 |
| Larry    | 1943-12-25 | 04:10:42  | 1943-12-25 04:10:42 |
| LarryCur | 2020-05-12 | 18:26:14  | 2020-05-12 18:26:14 |
+----------+------------+-----------+---------------------+
3 rows in set (0.00 sec)

mysql> SELECT DATEDIFF(NOW(), birthdate) FROM people;
+----------------------------+
| DATEDIFF(NOW(), birthdate) |
+----------------------------+
|                      13332 |
|                      27898 |
|                          0 |
+----------------------------+
3 rows in set (0.01 sec)

mysql> SELECT birthdt, DATE_ADD(birthdt, INTERVAL 1 MONTH) FROM people;
+---------------------+-------------------------------------+
| birthdt             | DATE_ADD(birthdt, INTERVAL 1 MONTH) |
+---------------------+-------------------------------------+
| 1983-11-11 10:07:35 | 1983-12-11 10:07:35                 |
| 1943-12-25 04:10:42 | 1944-01-25 04:10:42                 |
| 2020-05-12 18:26:14 | 2020-06-12 18:26:14                 |
+---------------------+-------------------------------------+
3 rows in set (0.00 sec)

mysql> SELECT birthdt, DATE_ADD(birthdt, INTERVAL 10 SECOND) FROM people;
+---------------------+---------------------------------------+
| birthdt             | DATE_ADD(birthdt, INTERVAL 10 SECOND) |
+---------------------+---------------------------------------+
| 1983-11-11 10:07:35 | 1983-11-11 10:07:45                   |
| 1943-12-25 04:10:42 | 1943-12-25 04:10:52                   |
| 2020-05-12 18:26:14 | 2020-05-12 18:26:24                   |
+---------------------+---------------------------------------+
3 rows in set (0.00 sec)

mysql> SELECT birthdt, DATE_ADD(birthdt, INTERVAL 3 QUARTER) FROM people;
+---------------------+---------------------------------------+
| birthdt             | DATE_ADD(birthdt, INTERVAL 3 QUARTER) |
+---------------------+---------------------------------------+
| 1983-11-11 10:07:35 | 1984-08-11 10:07:35                   |
| 1943-12-25 04:10:42 | 1944-09-25 04:10:42                   |
| 2020-05-12 18:26:14 | 2021-02-12 18:26:14                   |
+---------------------+---------------------------------------+
3 rows in set (0.00 sec)

mysql> SELECT birthdt, birthdt + INTERVAL 1 MONTH FROM people;
+---------------------+----------------------------+
| birthdt             | birthdt + INTERVAL 1 MONTH |
+---------------------+----------------------------+
| 1983-11-11 10:07:35 | 1983-12-11 10:07:35        |
| 1943-12-25 04:10:42 | 1944-01-25 04:10:42        |
| 2020-05-12 18:26:14 | 2020-06-12 18:26:14        |
+---------------------+----------------------------+
3 rows in set (0.00 sec)

mysql>
mysql> SELECT birthdt, birthdt - INTERVAL 5 MONTH FROM people;
+---------------------+----------------------------+
| birthdt             | birthdt - INTERVAL 5 MONTH |
+---------------------+----------------------------+
| 1983-11-11 10:07:35 | 1983-06-11 10:07:35        |
| 1943-12-25 04:10:42 | 1943-07-25 04:10:42        |
| 2020-05-12 18:26:14 | 2019-12-12 18:26:14        |
+---------------------+----------------------------+
3 rows in set (0.00 sec)

mysql> SELECT birthdt, birthdt + INTERVAL 15 MONTH + INTERVAL 10 HOUR FROM people;
+---------------------+------------------------------------------------+
| birthdt             | birthdt + INTERVAL 15 MONTH + INTERVAL 10 HOUR |
+---------------------+------------------------------------------------+
| 1983-11-11 10:07:35 | 1985-02-11 20:07:35                            |
| 1943-12-25 04:10:42 | 1945-03-25 14:10:42                            |
| 2020-05-12 18:26:14 | 2021-08-13 04:26:14                            |
+---------------------+------------------------------------------------+
3 rows in set (0.00 sec)
```

## TIMESTAMPS
```
mysql> CREATE TABLE comments (
    ->     content VARCHAR(100),
    ->     created_at TIMESTAMP DEFAULT NOW()
    -> );
Query OK, 0 rows affected (0.10 sec)

mysql> INSERT INTO comments (content) VALUES('lol what a funny article');
Query OK, 1 row affected (0.02 sec)

mysql>
mysql> INSERT INTO comments (content) VALUES('I found this offensive');
Query OK, 1 row affected (0.00 sec)

mysql>
mysql> INSERT INTO comments (content) VALUES('Ifasfsadfsadfsad');
Query OK, 1 row affected (0.02 sec)

mysql>
mysql> SELECT * FROM comments ORDER BY created_at DESC;
+--------------------------+---------------------+
| content                  | created_at          |
+--------------------------+---------------------+
| lol what a funny article | 2020-05-12 19:10:19 |
| I found this offensive   | 2020-05-12 19:10:19 |
| Ifasfsadfsadfsad         | 2020-05-12 19:10:19 |
+--------------------------+---------------------+
3 rows in set (0.01 sec)

mysql> CREATE TABLE comments2 (
    ->     content VARCHAR(100),
    ->     changed_at TIMESTAMP DEFAULT NOW() ON UPDATE CURRENT_TIMESTAMP
    -> );
Query OK, 0 rows affected (0.05 sec)

mysql>
mysql> INSERT INTO comments2 (content) VALUES('dasdasdasd');
Query OK, 1 row affected (0.00 sec)

mysql>
mysql> INSERT INTO comments2 (content) VALUES('lololololo');
Query OK, 1 row affected (0.01 sec)

mysql>
mysql> INSERT INTO comments2 (content) VALUES('I LIKE CATS AND DOGS');
Query OK, 1 row affected (0.02 sec)

mysql>
mysql> UPDATE comments2 SET content='THIS IS NOT GIBBERISH' WHERE content='dasdasdasd';
Query OK, 1 row affected (0.03 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM comments2;
+-----------------------+---------------------+
| content               | changed_at          |
+-----------------------+---------------------+
| THIS IS NOT GIBBERISH | 2020-05-12 19:11:16 |
| lololololo            | 2020-05-12 19:11:15 |
| I LIKE CATS AND DOGS  | 2020-05-12 19:11:15 |
+-----------------------+---------------------+
3 rows in set (0.00 sec)

mysql>
mysql> SELECT * FROM comments2 ORDER BY changed_at;
+-----------------------+---------------------+
| content               | changed_at          |
+-----------------------+---------------------+
| lololololo            | 2020-05-12 19:11:15 |
| I LIKE CATS AND DOGS  | 2020-05-12 19:11:15 |
| THIS IS NOT GIBBERISH | 2020-05-12 19:11:16 |
+-----------------------+---------------------+
3 rows in set (0.00 sec)
```
## Data Types Challenge
```
mysql> SELECT CURTIME();
+-----------+
| CURTIME() |
+-----------+
| 19:23:00  |
+-----------+
1 row in set (0.01 sec)

mysql> SELECT CURDATE();
+------------+
| CURDATE()  |
+------------+
| 2020-05-12 |
+------------+
1 row in set (0.00 sec)

mysql> SELECT DAYOFWEEK(CURDATE());
+----------------------+
| DAYOFWEEK(CURDATE()) |
+----------------------+
|                    3 |
+----------------------+
1 row in set (0.01 sec)

mysql> SELECT DAYOFWEEK(NOW());
+------------------+
| DAYOFWEEK(NOW()) |
+------------------+
|                3 |
+------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(NOW(), '%w') + 1;
+------------------------------+
| DATE_FORMAT(NOW(), '%w') + 1 |
+------------------------------+
|                            3 |
+------------------------------+
1 row in set (0.00 sec)

mysql> SELECT DAYNAME(NOW());
+----------------+
| DAYNAME(NOW()) |
+----------------+
| Tuesday        |
+----------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(NOW(), '%W');
+--------------------------+
| DATE_FORMAT(NOW(), '%W') |
+--------------------------+
| Tuesday                  |
+--------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(CURDATE(), '%m/%d/%Y');
+------------------------------------+
| DATE_FORMAT(CURDATE(), '%m/%d/%Y') |
+------------------------------------+
| 05/12/2020                         |
+------------------------------------+
1 row in set (0.00 sec)

Database changed
mysql> SELECT DATE_FORMAT(NOW(), '%M %D at %h:%i');
+--------------------------------------+
| DATE_FORMAT(NOW(), '%M %D at %h:%i') |
+--------------------------------------+
| May 12th at 07:26                    |
+--------------------------------------+
1 row in set (0.00 sec)

mysql>
mysql> CREATE TABLE tweets(
    ->     content VARCHAR(140),
    ->     username VARCHAR(20),
    ->     created_at TIMESTAMP DEFAULT NOW()
    -> );
Query OK, 0 rows affected (0.14 sec)

mysql> INSERT INTO tweets (content, username) VALUES('this is my first tweet', 'coltscat');
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM tweets;
+------------------------+----------+---------------------+
| content                | username | created_at          |
+------------------------+----------+---------------------+
| this is my first tweet | coltscat | 2020-05-12 19:27:02 |
+------------------------+----------+---------------------+
1 row in set (0.08 sec)

mysql>
mysql> INSERT INTO tweets (content, username) VALUES('this is my second tweet', 'coltscat');
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM tweets;
+-------------------------+----------+---------------------+
| content                 | username | created_at          |
+-------------------------+----------+---------------------+
| this is my first tweet  | coltscat | 2020-05-12 19:27:02 |
| this is my second tweet | coltscat | 2020-05-12 19:27:03 |
+-------------------------+----------+---------------------+
2 rows in set (0.00 sec)
```



