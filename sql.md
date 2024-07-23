- First take terminal and type : [ psql -U <userName> ] ,
 => will ask password => enter the password.

 - [ \l ] will all the databases existing.

 - [ \! cls ] = will clear the terminal

 - [ \c  ]

------------- To create a dataBase -----------------------
 - [ CREATE DATABASE <dataBase name>; ] = will create a table in the selected database. ---> { do not avoid the ; }

- [ \c <dataBase name> ] = will enter to that dataBase

- [ \d ] - when inside table , \d will display all tables , \l has no effect

-[ \d <tableName> ] - show only that particular table;

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


---------------------------- WHERE --------------------------------------

