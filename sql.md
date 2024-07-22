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

------------- To create a TABLE -----------------------
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




    