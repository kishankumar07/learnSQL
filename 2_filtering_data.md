Using WHERE :

            SELECT * FROM employee WHERE dob > '1992-01-01' ORDER BY name ASC;


 company=# select * from employee;

 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(6 rows)


company=# select * from employee where dob > '1992-01-01' order by name asc;
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
(5 rows)


-----------------------------------------------------------------------------------------


                    SELECT * FROM employee WHERE dob = '1992-05-03';

                    SELECT * FROM employee WHERE name = 'John';

                    SELECT dob,gender,place,id,name FROM employee WHERE place ='Assam';


company=# select*from employee where dob = '1992-05-03';
 id | name  |      email      |    dob     | gender | place
----+-------+-----------------+------------+--------+--------
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(2 rows)


---------------------------------------------------------------------------------

            SELECT * FROM employee WHERE name = 'John' AND dob <='1990-04-04';

company=# select*from employee where name = 'John' and dob <='1990-04-04';
 id | name |     email      |    dob     | gender |  place
----+------+----------------+------------+--------+---------
  1 | John | john@gmail.com | 1990-04-04 | M      | Kolkata
(1 row)


-------------------------------------------------------------------------------

            SELECT * FROM names WHERE first_name = 'Vishnu' AND last_name = 'G R';


company=# select * from names where first_name = 'Vishnu' and last_name = 'G R';
 first_name | last_name |       email
------------+-----------+--------------------
 Vishnu     | G R       | grvishnu@gmail.com
(1 row)


-----------------------------------------------------------------------------

                SELECT * FROM names WHERE first_name = 'Vishnu' OR last_name = 'Ravi';


company=# select * from names where first_name = 'Vishnu' OR last_name = 'Ravi';
 first_name | last_name |       email
------------+-----------+--------------------
 Vishnu     | G R       | grvishnu@gmail.com
 Aparna     | Ravi      | aparna@gmail.com
(2 rows)

----------------------------------------------------------------------------------------------

                SELECT * FROM names WHERE first_name IN ('Vishnu','Sahal','Aparna');

company=# select * from names where first_name IN ('John','Vishnu','Rajan');
 first_name | last_name |       email
------------+-----------+--------------------
 John       | Doe       | john@gmail.com
 Vishnu     | G R       | grvishnu@gmail.com
(2 rows)



------------------------------------------------------------------------------------------------


            SELECT * FROM employee WHERE email LIKE '%gmail%';


company=# select * from employee where email like '%gmail%';
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(6 rows)


company=# select * from employee where email like '%gmail%' AND gender = 'F';
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
(2 rows)


--------------------------------------------------------------------------------------------------

                SELECT name,LENGTH(name) len FROM employee WHERE name LIKE 'D%' AND LENGTH(name) BETWEEN 3 AND 5;



company=# SELECT name,LENGTH(name) len FROM employee WHERE name LIKE 'D%' AND LENGTH(name) BETWEEN 2 AND 5 ;
 name  | len
-------+-----
 Doe   |   3
 Divya |   5
(2 rows)


-----------------------------------------------------------------------------------------------------

                            SELECT name FROM employee WHERE email LIKE '%gmail%' AND gender <> 'M'';

company=# select name from employee where email like '%gmail%' AND gender <> 'M';
 name
-------
 Divya
 Priya
(2 rows)



-----------------------------------------------------------------------------------------------------




company=# select*from employee order by name;
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
(6 rows)


company=# select*from employee order by name offset 3;
 id | name  |      email      |    dob     | gender |  place
----+-------+-----------------+------------+--------+----------
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
(3 rows)


company=# select * from employee order by name offset 3 fetch first 2 rows only;
 id | name  |      email      |    dob     | gender | place
----+-------+-----------------+------------+--------+-------
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(2 rows)

company=# select * from employee order by name offset 2 fetch first 1 row only;
 id | name |     email      |    dob     | gender |  place
----+------+----------------+------------+--------+---------
  1 | John | john@gmail.com | 1990-04-04 | M      | Kolkata
(1 row)



--------------------------------------------------------------------------------------------------


                      SELECT * FROM employee WHERE name IN ('Sangham','Raj','Rahul','Divya');

Using IN:
to find any row using a string or number or anything just search this thing in the table

compared to LIKE , it check for a particular content in the table rows.

company=# select * from employee where name in ('Divya','John','Raj','Poulose');
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
(2 rows)

== The above query usign IN is replacable using OR :

                  SELECT * FROM employee WHERE name = 'Divya' OR name = 'John' OR name = 'Daniel';

company=# select*from employee where name = 'Divya' OR name = 'John' OR name = 'Varsha';
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
(2 rows)


---------------------------------------------------------------------------------------------


                SELECT * FROM employee WHERE name NOT IN ('John','Divya');

                (NOT IN)

company=# select * from employee where email not in ('john@gmail.com');
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(5 rows)


---------------------------------------------------------------------------------------------------


                    SELECT * FROM employee WHERE dob BETWEEN '1990-01-02' AND '1995-04-05' ORDER BY name;

Usage : BETWEEN

company=# select * from employee where dob between '1990-01-01' AND '2000-01-01' order by name;
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
(6 rows)


company=# select * from employee where dob between '1990-01-01' AND '1992-01-01' order by name;
 id | name |     email      |    dob     | gender |  place
----+------+----------------+------------+--------+---------
  1 | John | john@gmail.com | 1990-04-04 | M      | Kolkata
(1 row)


------------------------------------------------------------------------------------------


                          SELECT * FROM employee WHERE dob NOT BETWEEN '1990-01-01' AND '1992-01-01' ORDER BY name ASC;


Usage  : NOT BETWEEN

company=# select*from employee where dob not between '1990-01-01' and '1992-01-01';
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(5 rows)

company=# select*from employee where dob not between '1990-01-01' and '1992-01-01'And gender = 'F';
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
(2 rows)


-------------------------------------------------------------------------------------------------