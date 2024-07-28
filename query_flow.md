 =- Understanding the flow of SQL query execution helps in writing codes more efficiently for error free queries  :

 - it seems like it all starts from SELECT , but here is an example and you'll blow your mind : 




                    SELECT * FROM employess;

company=# select* from employees;
 id | name  |      email      | gender | created_at
----+-------+-----------------+--------+------------
  1 | Kiran | kiran@gmail.com | M      | 2024-07-28
  2 | Raju  | raju@gmail.com  | M      | 2024-07-28
  3 | Reji  | reji@gmail.com  | M      | 2024-07-28
  4 | Alex  | alex@gmail.com  | M      | 2024-07-28
  5 | Sam   | sam@gmail.com   | M      | 2024-07-28
(5 rows)

                    SELECT * FROM address;

company=# select*from address;
 id | emp_id |     city     |  district  |  pin
----+--------+--------------+------------+--------
  1 |      1 | Irinjalakuda | Thrissur   | 689898
  2 |      2 | Kodungallur  | Thrissur   | 383838
  3 |      3 | Tirur        | Malappuram | 787899
(3 rows)


-------------------------- Now I am going to write a complex query to demonstrate the actual work flow of the clauses :

            SELECT emp.id,emp.name,emp.email.addr.city,addr.district,addr.pin FROM employees AS emp INNER JOIN address AS addr ON emp.id = addr.emp_id GROUP BY emp.id,emp.name,emp.email,addr.city,addr.district,addr.pin HAVING (emp.id > 0) ORDER BY emp.name LIMIT 3;



 company=# select emp.id,emp.name,emp.email,add.city,add.district,add.pin from employees AS emp inner join address AS add on emp.id = add.emp_id where gender = 'M' group by emp.id,emp.name,emp.email,add.city,add,district,add.pin having (emp.id > 0) order by emp.name limit 3;
 id | name  |      email      |     city     |  district  |  pin
----+-------+-----------------+--------------+------------+--------
  1 | Kiran | kiran@gmail.com | Irinjalakuda | Thrissur   | 689898
  2 | Raju  | raju@gmail.com  | Kodungallur  | Thrissur   | 383838
  3 | Reji  | reji@gmail.com  | Tirur        | Malappuram | 787899
(3 rows)

--------------------------------------------------------------------------------------------------------------

1 ) FROM  : Determines the source tables.
- Determines all the source tables . This step identifies all the tables involved in the query.
- Intermediate result : All the rows from 'employees' and 'address' before any filtering or joining.


2 ) JOIN : Join the tables if there is any join operations.
3 ) ON   : Apply the join condition
- Based on the JOIN and ON , like it will match the rows based on the condition given in ON , those matched rows will be combined.
- Still all the columns are there , only rows are combined of the whole 2 tables.


4 ) WHERE : Filter the rows based on any specified conditions
- Now we have some rows from 2 tables, to this coniditon of WHERE is applied, so again filtration happens. -> news rows from filtration is got.

5 ) GROUP BY : Group the rows by specified columns.
- Filtered rows are grouped based on the columns given here -> emp.id,emp.name,emp.email,addr.city,addr.district,addr.pin  -> based on these columns they are grouped

6 ) HAVING : Filter groups based on specified conditions.
- from the GROUP BY the coulmns where grouped and to this condition is applied to filter rows again.

7 ) SELECT : Select the specified columns or expressions.
- See this SELECT comes here at 7th step, this means the actual result that will be displayed is based on not any other clauses, it is based on this SELECT

8 ) DISTINCT : Remove any duplicates from the Result.
- From this selected columns if any rows are duplicates, they will be distintified

9 ) ORDRE BY : Sort the results by specified columns or expressions.
- Based on what columns or expression the column outputs rows will be ordered 


10 ) LIMIT / OFFSET : Limit the number of rows at result / skip specified rows.
- Finally the number of output result is out !

---------------------------------------------------------------------------------------------------------------



                        LEFT JOIN 


            SELECT emp.id,emp.name,emp.email,addr.city,addr.district,addr.pin FROM employees AS emp LEFT JOIN address AS addr ON emp.id = addr.emp_id;



company=# select emp.id,emp.name,emp.email,addr.city,addr.district,addr.pin from employees as emp left join address as addr on emp.id = addr.emp_id;
 id | name  |      email      |     city     |  district  |  pin
----+-------+-----------------+--------------+------------+--------
  1 | Kiran | kiran@gmail.com | Irinjalakuda | Thrissur   | 689898
  2 | Raju  | raju@gmail.com  | Kodungallur  | Thrissur   | 383838
  3 | Reji  | reji@gmail.com  | Tirur        | Malappuram | 787899
  5 | Sam   | sam@gmail.com   |              |            |
  4 | Alex  | alex@gmail.com  |              |            |
(5 rows)


-----------------------------------------------------------------------------------------------------------------------


                                    RIGHT JOIN

         SELECT emp.id,emp.name,emp.email,addr.city,addr.district,addr.pin FROM employees AS emp RIGHT JOIN address AS addr ON emp.id = addr.emp_id;                                    

-----------------------------------------------------------------------------------------------------------         

