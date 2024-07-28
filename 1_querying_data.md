- First take terminal and type : [ psql -U <userName> ] ,
 => will ask password => enter the password.

 - [ \l ] will show all the databases existing.

 - [ \! cls ] = will clear the terminal

 - [ \c  ]

------------- To create a dataBase -----------------------
 - [ CREATE DATABASE <dataBase name>; ] = will create a table in the selected database. ---> { do not avoid the ; }

- [ \c <dataBase name> ] = will enter to that dataBase

- [ \d ] - when inside table , \d will display all tables , \l has no effect

-[ \d <tableName> ] - show only that particular table;

-[DROP DATABASE <database name>] = Delete the database;

------------- To create a TABLE no_constraint -----------------------
CREATE TABLE <tableName>(
    id INT,
    name VARCHAR(50),
    email VARCHAR(50),
    date_of_birth DATE);

    {  this will create a table with name <tableName> };
    { To see only this table from the list of all tables inside the database created : \d <tableName> }
------------------------------------- end -------------------------------

----------- To delete a TABLE-------------
- [ DROP TABLE <tableName>; ] --> don't forget the ;


-------------------- CREATE A TABLE with Constranits -----------------------------

        CREATE TABLE employees(
            id BIGSERIAL NOT NULL PRIMARY KEY,
            name VARCHAR(50)  NOT NULL,
            email VARCHAR(50) NOT NULL UNIQUE,
            date_of_birth DATE
        );
done deal
---------------------------------------------------------------------------------        


---*&&*&*&*&*&*&*&&**&*&*&*&*&&*&*&*&*&*&*&*&*&*&*&*&*&*----------------------------

                    SELECT

 **/Once inserted all entries to fill in the table, if you want to see it :**

                SELECT * FROM employees;

id | name |   email        | date_of_birth
---+------+----------------+--------------
1  | John | john@gmail.com | 1990-01-01   
2  | Doe  | doe@gmail.com  | 1990-02-03
3  | Rose | rose@gmail.com | 1997-05-04

in the above format it will be displayed


----------------------------------------------------------------------------


company=# SELECT * FROM employee;
 id | name  |      email      | date_of_birth | gender
----+-------+-----------------+---------------+--------
  1 | John  | john@gmail.com  | 1990-01-02    | male
  2 | Doe   | doe@gmail.com   | 1991-03-02    | male
  3 | Rose  | rose@gmail.com  | 1993-05-06    | female
  4 | Jack  | jack@gmail.com  | 1995-05-23    | male
  5 | Alice | alice@gmail.com | 2001-06-13    | female
(5 rows)

In the above case, if only  columns like :  id | name | email | gender is needed or otherwise date_of_birth is not needed then :

                                    ||
                                    \/
                                      
                SELECT id,name,email,gender FROM employee;

                                    ||
                                    \/
company=# SELECT id,name,email,gender FROM employee;
 id | name  |      email      | gender
----+-------+-----------------+--------
  1 | John  | john@gmail.com  | male
  2 | Doe   | doe@gmail.com   | male
  3 | Rose  | rose@gmail.com  | female
  4 | Jack  | jack@gmail.com  | male
  5 | Alice | alice@gmail.com | female
(5 rows)



--------------------------------------------------------------------------------------

                SELECT name FROM employees;
----
John
Doe
Rose
(3 Rows)                

--------------------------------------------------------------------------------------

                SELECT date_of_birth FROM employees;

------
 1990-01-01
 1992-01-03
 1995-03-03
(3 Rows)

------------------------------------------------------------------------------------

                SELECT name,email FROM employees;

name | email
-----+------------
John | john@gmail.com
Doe  | doe@gmail.com
Rose | rose@gmail.com                

--------------------------------------------------------------------------------------

                SELECT * FROM employees ORDER BY name ASC;

id | name |   email         | date_of_birth
---+------+-----------------+--------------
1  | Doe  | doe@gmail.com   | 1990-02-03   
2  | John | john@gmail.com  | 1990-01-01
3  | Rose | rose@gmail.com  | 1997-05-04                

-----------------------------------------------------------------------------------------

                SELECT * FROM employees ORDER BY name DESC;

id | name |   email        | date_of_birth
---+------+----------------+--------------
1  | Rose | rose@gmail.com | 1997-05-04   
2  | John | john@gmail.com | 1990-01-01
3  | Doe  | doe@gmail.com  | 1990-02-03                

--------------------------------------------------------------------------------------------

existing table : 

id | name |   email        | date_of_birth
---+------+----------------+--------------
1  | John | john@gmail.com | 1990-01-01   
2  | Doe  | doe@gmail.com  | 1990-02-03
3  | Rose | rose@gmail.com | 1997-05-04     
4  | Jack | jack@gmail.com | 1990-01-01

{see here I added one more field as entry 4 for Jack, 
 question : Display all the date of births only but *unique* - because Jack and John has same date-of-birth}

                SELECT DISTINCT date_of_birth FROM employees;

------------------------------------------------------------------------------------------------                

Difference between \d and \dt =>

\d :
- The \d command is a general-purpose command to describe database objects.
- When used without any arguments, it lists all tables, views, sequences, and indexes in the current database.
- When used with a table name (e.g., \d employees), it provides detailed information about the structure of that specific table, including columns, data types, indexes, constraints, and any other relevant details.

company=# \d
               List of relations
 Schema |       Name        |   Type   |  Owner   
--------+-------------------+----------+----------
 public | employees          | table    | postgres
 public | employees_id_seq   | sequence | postgres

--==--==--==--==--==--==--==--==--==


\dt :
The \dt command is specifically used to list tables.
When used without any arguments, it lists all tables in the current schema.
It provides a summary of tables, including their names, owners, and schemas, but does not provide detailed information about the structure of each table.

company=# \d employees
                                   Table "public.employees"
    Column     |         Type          | Collation | Nullable |                Default
---------------+-----------------------+-----------+----------+---------------------------------------
 id            | bigint                |           | not null | nextval('employees_id_seq'::regclass)
 name          | character varying(50) |           | not null |
 email         | character varying(50) |           | not null |
 date_of_birth | date                  |           |          |
Indexes:
    "employees_pkey" PRIMARY KEY, btree (id)
    "employees_email_key" UNIQUE CONSTRAINT, btree (email)


--==-==-=-=-=-=-=-=-==-=-=-=-=-=-=-=-=-=-=-=-=-=-=

company=# \dt
               List of relations
 Schema |       Name        | Type  |  Owner   
--------+-------------------+-------+----------
 public | employees          | table | postgres


----------------------------------------------------------------

To fetch only male /female :

            SELECT * FROM employee WHERE gender = 'female';


company=# SELECT * FROM employee WHERE gender='male';
 id |  name  |      email       | date_of_birth | gender
----+--------+------------------+---------------+--------
  1 | John   | john@gmail.com   | 1990-01-02    | male
  2 | Doe    | doe@gmail.com    | 1991-03-02    | male
  4 | Jack   | jack@gmail.com   | 1995-05-23    | male
  6 | Daniel | daniel@gmail.com | 1991-03-02    | male
(4 rows)


company=# SELECT * FROM employee WHERE gender = 'female';
 id | name  |      email      | date_of_birth | gender
----+-------+-----------------+---------------+--------
  3 | Rose  | rose@gmail.com  | 1993-05-06    | female
  5 | Alice | alice@gmail.com | 2001-06-13    | female
(2 rows)

--------------------------------------------------------------------------------

If need only the "Row of a Person" :
                
                SELECT * FROM employee WHERE name = "John";

company=# SELECT * FROM employee WHERE name = 'John';
 id | name |     email      | date_of_birth | gender
----+------+----------------+---------------+--------
  1 | John | john@gmail.com | 1990-01-02    | male
(1 row)

---------------------------------------------------------------------------------            


                SELECT * FROM employees WHERE date_of_birth = '1993-05-06';

company=# SELECT * FROM employee WHERE date_of_birth = '1993-05-06';
 id | name |     email      | date_of_birth | gender
----+------+----------------+---------------+--------
  3 | Rose | rose@gmail.com | 1993-05-06    | female
(1 row)

----------------------------------------------------------------------------------

                    SELECT * FROM employee WHERE name = 'Rose' AND gender='female';
AND:
company=# SELECT * FROM employee WHERE gender='female' AND name='Rose';
 id | name |     email      | date_of_birth | gender
----+------+----------------+---------------+--------
  3 | Rose | rose@gmail.com | 1993-05-06    | female
(1 row)

----------------------------------------------------------------------------------------

                    SELECT * FROM employee WHERE name='Elisa' OR gender='female';
OR:
company=# SELECT * FROM employee WHERE gender='female' OR name='Elisa';
 id | name  |      email      | date_of_birth | gender
----+-------+-----------------+---------------+--------
  3 | Rose  | rose@gmail.com  | 1993-05-06    | female
  5 | Alice | alice@gmail.com | 2001-06-13    | female
(2 rows)

------------------------------------------------------------------------------------------

        SELECT * FROM employee WHERE date_of_birth < '2001-04-05';

< or > operator :
company=# SELECT * FROM employee WHERE date_of_birth<'2004-04-05';
 id |  name  |      email       | date_of_birth | gender
----+--------+------------------+---------------+--------
  1 | John   | john@gmail.com   | 1990-01-02    | male
  2 | Doe    | doe@gmail.com    | 1991-03-02    | male
  3 | Rose   | rose@gmail.com   | 1993-05-06    | female
  4 | Jack   | jack@gmail.com   | 1995-05-23    | male
  5 | Alice  | alice@gmail.com  | 2001-06-13    | female
  6 | Daniel | daniel@gmail.com | 1991-03-02    | male
(6 rows)


------------------------------------------------------------------------------------------------


                          SELECT * FROM employee LIMIT 2;


company=# SELECT * FROM employee;
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(6 rows)


company=# SELECT * FROM employee LIMIT 2;
 id | name |     email      |    dob     | gender |  place
----+------+----------------+------------+--------+---------
  1 | John | john@gmail.com | 1990-04-04 | M      | Kolkata
  2 | Doe  | doe@gmail.com  | 1992-05-03 | M      | Punjab
(2 rows)


------------------------------------------------------------------------------------


                          SELECT first_name || ' ' || last_name,email FROM names;
                          

This is about concatenation :


                      company=# SELECT * FROM names;
 first_name | last_name |       email
------------+-----------+--------------------
 John       | Doe       | john@gmail.com
 Rahul      | Renjan    | rahul@gmail.com
 Vishnu     | G R       | grvishnu@gmail.com
 Aparna     | Ravi      | aparna@gmail.com
 Abhijith   | K Anand   | abhijith@gmail.com
(5 rows)


                          ||
                          \/


company=# SELECT first_name || ' ' || last_name,email FROM names;
     ?column?     |       email
------------------+--------------------
 John Doe         | john@gmail.com
 Rahul Renjan     | rahul@gmail.com
 Vishnu G R       | grvishnu@gmail.com
 Aparna Ravi      | aparna@gmail.com
 Abhijith K Anand | abhijith@gmail.com
(5 rows)


                          ||
                          \/

company=# SELECT first_name || ' ' || last_name AS full_name,email FROM names;
     full_name     |       email
------------------+--------------------
 John Doe         | john@gmail.com
 Rahul Renjan     | rahul@gmail.com
 Vishnu G R       | grvishnu@gmail.com
 Aparna Ravi      | aparna@gmail.com
 Abhijith K Anand | abhijith@gmail.com
(5 rows)

--------------------------------------------------------------------------------------

              SELECT now();
returns the current date and time of the pSQL server.

company=# select now();
               now
---------------------------------
 2024-07-24 14:52:51.87828+05:30
(1 row)

-----------------------------------------------------------------------------------------



                SELECT id,name AS full_name,email,dob,gender,place FROM employee;


This is column aliasing : here "name" was replaced with full_name

company=# SELECT * FROM employee;
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(6 rows)


company=# SELECT id,name AS full_name,email,dob,gender,place from employee;
 id | full_name |      email      |    dob     | gender |   place
----+-----------+-----------------+------------+--------+-----------
  1 | John      | john@gmail.com  | 1990-04-04 | M      | Kolkata
  2 | Doe       | doe@gmail.com   | 1992-05-03 | M      | Punjab
  3 | Divya     | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya     | priya@gmail.com | 1999-12-25 | F      | Noida
  5 | Raja      | raj@gmail.com   | 1993-11-12 | M      | Rajastan
  6 | Rahul     | rahul@gmail.com | 1992-05-03 | M      | Assam
(6 rows)



----------------------------------------------------------------------------


                        SELECT email,dob AS date_of_birth,gender,place,id,name AS full_name FROM employee;


this query has 2 concepts : 1-> in which order the output has to come is defined , see the order

2-> aliasing is done using "AS", name AS full_name will be replaced by full_name after query.

company=# SELECT * FROM employee;
 id | name  |      email      |    dob     | gender |   place
----+-------+-----------------+------------+--------+-----------
  1 | John  | john@gmail.com  | 1990-04-04 | M      | Kolkata
  2 | Doe   | doe@gmail.com   | 1992-05-03 | M      | Punjab
  3 | Divya | divya@gmail.com | 1997-05-05 | F      | Jharkhand
  4 | Priya | priya@gmail.com | 1999-12-25 | F      | Noida
  5 | Raja  | raj@gmail.com   | 1993-11-12 | M      | Rajastan
  6 | Rahul | rahul@gmail.com | 1992-05-03 | M      | Assam
(6 rows)


company=# SELECT email,dob AS date_of_birth,gender,place,id,name FROM employee;
      email      | date_of_birth | gender |   place   | id | name
-----------------+---------------+--------+-----------+----+-------
 john@gmail.com  | 1990-04-04    | M      | Kolkata   |  1 | John
 doe@gmail.com   | 1992-05-03    | M      | Punjab    |  2 | Doe
 divya@gmail.com | 1997-05-05    | F      | Jharkhand |  3 | Divya
 priya@gmail.com | 1999-12-25    | F      | Noida     |  4 | Priya
 raj@gmail.com   | 1993-11-12    | M      | Rajastan  |  5 | Raja
 rahul@gmail.com | 1992-05-03    | M      | Assam     |  6 | Rahul
(6 rows)

Purpose of Aliasing : To make heading of the output of a query more meaningful;


--------------------------------------------------------------------------------------------

                    SELECT first_name || ' ' || last_name AS full_name FROM names ORDER BY last_name DESC; 


the approach is : 1) concat first name and last name and alias : full_name , now this output is again sorted in descending order based on last name;


company=# SELECT * FROM names;
 first_name | last_name |       email
------------+-----------+--------------------
 John       | Doe       | john@gmail.com
 Rahul      | Renjan    | rahul@gmail.com
 Vishnu     | G R       | grvishnu@gmail.com
 Aparna     | Ravi      | aparna@gmail.com
 Abhijith   | K Anand   | abhijith@gmail.com
(5 rows)


company=# SELECT first_name || ' ' || last_name AS full_name,email FROM names ORDER BY last_name DESC;
    full_name     |       email
------------------+--------------------
 Rahul Renjan     | rahul@gmail.com
 Aparna Ravi      | aparna@gmail.com
 Abhijith K Anand | abhijith@gmail.com
 Vishnu G R       | grvishnu@gmail.com
 John Doe         | john@gmail.com
(5 rows)


-----------------------------------------------------------------------------------

        SELECT first_name,LENGTH(first_name) len FROM names ORDER BY len DESC;

bulb : only one column is chosen : first_name and its lenght is found then sorted in descending at last using length property.


company=# select * from names;
 first_name | last_name |       email
------------+-----------+--------------------
 John       | Doe       | john@gmail.com
 Rahul      | Renjan    | rahul@gmail.com
 Vishnu     | G R       | grvishnu@gmail.com
 Aparna     | Ravi      | aparna@gmail.com
 Abhijith   | K Anand   | abhijith@gmail.com
(5 rows)


                            ||
                            \/


company=# SELECT first_name,LENGTH(first_name) len FROM names ORDER BY len DESC;
 first_name | len
------------+-----
 Abhijith   |   8
 Vishnu     |   6
 Aparna     |   6
 Rahul      |   5
 John       |   4
(5 rows)

ORDER BY is evaluated after the SELECT , ths column alias "len" will be there so they can be soreted in ascending or descending order.


