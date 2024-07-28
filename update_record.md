- In this tutorial we will learn about updating a field from a table :

I shall show with an example, as I infer you already knows the syntax :


1) 

                    SELECT * FROM fizz;

company=# select*from fizz;
 id | name |     email     | gender | created_at
----+------+---------------+--------+------------
  1 | John | joe@gmail.com | M      | 2024-07-27
  2 | Doe  | doe@gmail.com | M      | 2024-07-27
(2 rows)

                    UPDATE fizz SET email = 'john@gmail.com' WHERE id= 1;

                    SELECT * FROM fizz;

company=# update fizz set email = 'john@gmail.com' where id = 1;
UPDATE 1
company=# select*from fizz;
 id | name |     email      | gender | created_at
----+------+----------------+--------+------------
  2 | Doe  | doe@gmail.com  | M      | 2024-07-27
  1 | John | john@gmail.com | M      | 2024-07-27
(2 rows)



================= Now you learnt how to edit a particular field in a table using the uique id ! ------------------------


2) if you wish to update **multiple fields** at a time ;

                            SELECT * FROM fizz;

company=# select*from fizz;
 id | name |     email      | gender | created_at
----+------+----------------+--------+------------
  2 | Doe  | doe@gmail.com  | M      | 2024-07-27
  1 | John | john@gmail.com | M      | 2024-07-27
(2 rows)

                            UPDATE fizz SET email = 'arjun@hotmail.com',name='Arjun' WHERE id = 2;

                            SELECT * FROM fizz;


company=# update fizz set email = 'arjun@hotmail.com',name= 'Arjun' where id = 2;
UPDATE 1
company=# select * from fizz;
 id | name  |       email       | gender | created_at
----+-------+-------------------+--------+------------
  1 | John  | john@gmail.com    | M      | 2024-07-27
  2 | Arjun | arjun@hotmail.com | M      | 2024-07-27
(2 rows)


company=#


---------------------------------  gReat work, now you can update multiple fields at time using , seperated------------------


