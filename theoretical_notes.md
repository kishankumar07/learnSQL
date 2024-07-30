
-ACID properties = Those properties that ensures that all transactions taking place in a database in consistent.

- Atomicity,Consistency,Isolation,Durability


------------------------------
- Atomicity = It ensures that a transaction is all-or-nothing. => either a transaction will fully complete or not at all. => if any part fail it is rolled back to previous state(database).

example : 

: Postgres uses BEGIN, COMMIT and ROLLBACK commands to manage transactions,
: When it is stated with BEGIN, postgreSQL ensures that changes are not visible to other transactions until COMMIT is issued.
:If there is any error or if explicitly issued ROLLBACK, then all changes made in the transaction is undone.


-----------------------
- Consistency = It ensures that a transaction takes a database from one valid state to another. or the database should be consistent before and after the transaction.
eg: data written to the db should be valid for the defined set of rules,like constraints


CREATE TABLE accounts (
    account_id SERIAL PRIMARY KEY,
    balance NUMERIC CHECK (balance >= 0)
);

BEGIN;

INSERT INTO accounts (balance) VALUES (-100); -- This will fail due to the CHECK constraint

COMMIT; -- This won't be reached, as the transaction will rollback due to the constraint violation


-------------------------

Isolation : Ensures operation of one transaction is isolated from other transactions, prevents interference with each other.

-------------------------

Durability : If any transactions are happened those changes have to be commited permanently to the db,even if any system crash.


-----------------------

                            NORMALIZATION

Normalization is the process of organizing data into database to reduce redundancy and improving data integrity.
: Dividing the database into smaller tables and defining relationships between these tables. 
: main goal is to store each piece of data only in one place, so efficient and efficient to maintain.                            


--------------------- 
                    WHERE and HAVING
                - WHERE is used to filter rows before aggregation.
                - HAVING -> filter rows after aggregation.

question : Count the number of employees in each department with more than 5 employees :

                    SELECT department , COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;


-----------------------

question : Find the department with the highest average salary :

                  SELECT department,avg(salary) FROM employees GROUP BY department order by avg(salary) DESC LIMIT 1;

                                            OR

                  SELECT department,avg(sum) AS average_salary FROM employees GROUP BY department ORDER BY average_salary DESC LIMIT 1;

---------------------------

Question 2: Find the employee(s) with the highest salary in each department:

                   SELECT department, name, salary
                            FROM employees e
                            WHERE salary = (
                                        SELECT MAX(salary)
                                        FROM employees
                                        WHERE department = e.department
                                    );


-----------------------------

                                salesperson | region  | amount
                             ------------+---------+-------
                                Alice       | North   | 100
                                Bob         | South   | 200
                                Alice       | North   | 150
                                Bob         | South   | 250
                                Charlie     | East    | 300



1)To find the total sales made by each salesperson:


                    SELECT salesperson,sum(amount) FROM sales GROUP BY salesperson

2) Find the total sales in each Region: 

                    SELECT region, sum(amount) FROM sales GROUP BY region;

--------------------------------


                            Tips to remember when using GROUP BY

1) Non-Aggregated Columns: Any column in the SELECT statement that is not inside an aggregate function must be included in the GROUP BY clause.
2) Order of Execution: The GROUP BY clause is processed after the WHERE clause but before the HAVING clause and the SELECT statement.
3) HAVING Clause: Use the HAVING clause to filter groups based on aggregate functions.

--------------------------------