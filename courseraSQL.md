SQL : Insert :=>

- INSERT statement inserts a row into a table.

        INSERT INTO users (name,email) VALUES ('Chuck','chuck@gmail.com');
        INSERT INTO users (name,email) VALUES ('Smith','smith@gmail.com')

----------------------------------------------------- 

SQL : Delete :=>

        DELETE FROM users WHERE email = 'smith@gmail.com';

----------------------------------------------------


SQL : Update :=>

Allows the updating of a field with a WHERE clause

        UPDATE users SET name= 'Charles' WHERE email='smith@gmail.com';

--------------------------------------------------------------

Retrieving Records : Select

Retrieves a group of Records= You can either retieve all the records or a subset of the records where a WHERE clause

                     SELECT * FROM users;

        SELECT * FROM users WHERE email='smith@gmail.com';


-----------------------------------------------------------------

Sorting with ORDER BY

You can add an ORDER BY clause to SELECT statements to get the results sorted in ascending or descending order

            SELECT * FROM users ORDER BY email;

--------------------------------------------------------------------

LIKE Clause

We can do wildcard matching in a WHERE clause using the LIKE operator

        SELECT * FROM users WHERE name LIKE '%e';

-----------------------------------------------------------------------     

The LIMIT/OFFSET Clauses
- We can request the first 'n' rows, or the first 'n' rows after skipping some rows.
- The WHERE and ORDER BY clauses happen *before* the LIMIT / OFFSET are applied.
- The OFFSET starts from row 0

        SELECT * FROM users ORDER BY email DESC LIMIT 2;
        SELECT * FROM users ORDER BY email OFFSET 1 LIMIT 2;

-----------------------------------------------------------------------
Counting Rows with SELECT

You can request to receive the count of the rows that would be retrieved instead of the rows.

        SELECT COUNT (*) FROM users;
        SELECT COUNT (*) FROM users WHERE email= 'smith@gmail.com';

----------------------------------------------------------------------        