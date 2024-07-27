

                ALTER TABLE employee ADD COLUMN salary NUMERIC DEFAULT 0;

                UPDATE employee SET salary = 50000 WHERE id = 1;
                
                UPDATE employee SET salary = 60000 WHERE id = 2;


                ALTER TABLE students ADD COLUMN email VARCHAR(100);



UPDATE students SET email = 'nicholas@example.com' WHERE id = 1;
UPDATE students SET email = 'rajappa@example.com' WHERE id = 2;
UPDATE students SET email = 'bholu@example.com' WHERE id = 3;
UPDATE students SET email = 'jaggu@example.com' WHERE id = 4;
UPDATE students SET email = 'machu@example.com' WHERE id = 5;
UPDATE students SET email = 'bheem@example.com' WHERE id = 6;
UPDATE students SET email = 'kaliya@example.com' WHERE id = 7;
UPDATE students SET email = 'indhu@example.com' WHERE id = 8;
UPDATE students SET email = 'mitali@example.com' WHERE id = 9;
UPDATE students SET email = 'divya@example.com' WHERE id = 10;




---------------------------------------------------------------------------------------------------------



company=# select * from students;
 id |   name   | mark | total
----+----------+------+-------
  1 | Nicholas |   89 |   200
  2 | Rajappa  |   34 |   100
  3 | Bholu    |   35 |   222
  4 | Jaggu    |   64 |   344
  5 | Machu    |   45 |   454
  6 | Bheem    |   23 |   222
  7 | Kaliya   |   65 |   555
  8 | Indhu    |   55 |   444
  9 | Mitali   |   77 |   777
 10 | Divya    |   66 |   765
(10 rows)


-= on this above table we are going to do this operation,

question : need another column as output that shows the percentage of each student in the rows as an aliased output ?


                    SELECT id,name,mark,total,(mark::float/total)*100 AS Percentage from students;



company=# select id,name,mark,total,(mark::float/total)*100 AS percentage from students;
 id |   name   | mark | total |     percentage
----+----------+------+-------+--------------------
  1 | Nicholas |   89 |   200 |               44.5
  2 | Rajappa  |   34 |   100 |                 34
  3 | Bholu    |   35 |   222 | 15.765765765765765
  4 | Jaggu    |   64 |   344 |   18.6046511627907
  5 | Machu    |   45 |   454 |  9.911894273127754
  6 | Bheem    |   23 |   222 |  10.36036036036036
  7 | Kaliya   |   65 |   555 | 11.711711711711711
  8 | Indhu    |   55 |   444 | 12.387387387387387
  9 | Mitali   |   77 |   777 |   9.90990990990991
 10 | Divya    |   66 |   765 |  8.627450980392156
(10 rows)

-------------------------------------------------------------------------------------------------------------------


question ) : to this table: Add a new column to it "email".

company=# select * from students;
 id |   name   | mark | total
----+----------+------+-------
  1 | Nicholas |   89 |   200
  2 | Rajappa  |   34 |   100
  3 | Bholu    |   35 |   222
  4 | Jaggu    |   64 |   344
  5 | Machu    |   45 |   454
  6 | Bheem    |   23 |   222
  7 | Kaliya   |   65 |   555
  8 | Indhu    |   55 |   444
  9 | Mitali   |   77 |   777
 10 | Divya    |   66 |   765
(10 rows)



ans :::::::------------------

company=# alter table students add column email varchar(210);
ALTER TABLE
company=# select * from students;
 id |   name   | mark | total | email
----+----------+------+-------+-------
  1 | Nicholas |   89 |   200 |
  2 | Rajappa  |   34 |   100 |
  3 | Bholu    |   35 |   222 |
  4 | Jaggu    |   64 |   344 |
  5 | Machu    |   45 |   454 |
  6 | Bheem    |   23 |   222 |
  7 | Kaliya   |   65 |   555 |
  8 | Indhu    |   55 |   444 |
  9 | Mitali   |   77 |   777 |
 10 | Divya    |   66 |   765 |
(10 rows)


question ) -- To this only add emails for id's 8,9,10 ?


company=# update students set email = 'indu@gmail.com' where id = 8;
UPDATE 1
company=# update students set email = 'mitali@gmail.com' where id = 9;
UPDATE 1
company=# update students set email = 'divya@gmail.com' where id = 10;
UPDATE 1
company=# select * from students;
 id |   name   | mark | total |      email
----+----------+------+-------+------------------
  1 | Nicholas |   89 |   200 |
  2 | Rajappa  |   34 |   100 |
  3 | Bholu    |   35 |   222 |
  4 | Jaggu    |   64 |   344 |
  5 | Machu    |   45 |   454 |
  6 | Bheem    |   23 |   222 |
  7 | Kaliya   |   65 |   555 |
  8 | Indhu    |   55 |   444 | indu@gmail.com
  9 | Mitali   |   77 |   777 | mitali@gmail.com
 10 | Divya    |   66 |   765 | divya@gmail.com
(10 rows)


--------------------------------------------------------------------------------------------------------------

                                    \COALESCE keyword

question ) explain COALESCE keyword?                                     

PostgreSQL COALESCE :

To handle NULL values in PostgreSQL , this COALESCE keyword is used.

To demonstrate : 

company=# select * from students;
 id |   name   | mark | total |      email
----+----------+------+-------+------------------
  1 | Nicholas |   89 |   200 |
  2 | Rajappa  |   34 |   100 |
  3 | Bholu    |   35 |   222 |
  4 | Jaggu    |   64 |   344 |
  5 | Machu    |   45 |   454 |
  6 | Bheem    |   23 |   222 |
  7 | Kaliya   |   65 |   555 |
  8 | Indhu    |   55 |   444 | indu@gmail.com
  9 | Mitali   |   77 |   777 | mitali@gmail.com
 10 | Divya    |   66 |   765 | divya@gmail.com
(10 rows)


To the above table , to handle the NULL values efficiently , we use COALESCE keyword, now see me in action: 


                        SELECT id,name,COALESCE(email,'email not found') FROM students;

company=# select id,name,coalesce(email,'email not found') from students;
 id |   name   |     coalesce
----+----------+------------------
  1 | Nicholas | email not found
  2 | Rajappa  | email not found
  3 | Bholu    | email not found
  4 | Jaggu    | email not found
  5 | Machu    | email not found
  6 | Bheem    | email not found
  7 | Kaliya   | email not found
  8 | Indhu    | indu@gmail.com
  9 | Mitali   | mitali@gmail.com
 10 | Divya    | divya@gmail.com
(10 rows)



2) Question : give another example :
source : geeksforgeeks

company=# select * from items;
 product | price | discount
---------+-------+----------
 A       |  1000 |       10
 B       |  1500 |       20
 C       |   800 |        5
 D       |   500 |
(4 rows)


company=# select product,(price-coalesce(discount,0)) from items;
 product | ?column?
---------+----------
 A       |      990
 B       |     1480
 C       |      795
 D       |      500
(4 rows)

3_) give another example ; 


company=# select * from items;
 product | price | discount
---------+-------+----------
 A       |  1000 |       10
 B       |  1500 |       20
 C       |   800 |        5
 D       |   500 |
(4 rows)


company=# select coalesce(discount,0) from items;
 coalesce
----------
       10
       20
        5
        0
(4 rows)



-----------------------------------------------------------------------------------------------------------------


                                    SELECT NOW();

DATE and Time :

company=# select now();
               now
---------------------------------
 2024-07-27 09:20:59.97563+05:30
(1 row)

this will print current date and time

2) To get the date only :


                                SELECT NOW()::DATE;

company=# select now()::date;
    now
------------
 2024-07-27
(1 row)


3) to get time :
                                    SELECT NOW()::TIME;            

company=# select now()::time;
      now
----------------
 09:23:54.42363
(1 row)


4) To get the year : 

                                    SELECT EXTRACT (YEAR FROM NOW());

company=# select extract(year from now());
 extract
---------
    2024
(1 row)


5) To get the month :

                                SELECT EXTRACT(MONTH FROM NOW());

company=# select extract (month from now());
 extract
---------
       7
(1 row)

6) find the current day :

                                SELECT EXTRACT (DAY FROM NOW());

company=# select extract(day from now());
 extract
---------
      27
(1 row)


7) To get a date 10 years later :

                                SELECT NOW() + INTERVAL '10 years';


company=# select now() + interval '10 years';
             ?column?
----------------------------------
 2034-07-27 09:29:46.727075+05:30
(1 row)

8) give the date 10 years before ; 


                                SELECT NOW - INTERVAL '10 years';

company=# select now() - interval '10 years';
             ?column?
----------------------------------
 2014-07-27 09:31:11.807294+05:30
(1 row)



-----------------------------------------------------------------------------------------------------------------