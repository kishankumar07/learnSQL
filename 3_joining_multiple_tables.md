
                SELECT b AS s_no,pname AS product_name,cname AS category_name FROM products INNER JOIN category ON a = category_id;

between SELECT and FROM the fields need to be shown in the output is said
also aliases are said using AS.


company=# select b AS s_No,pname AS product_name,cname AS category_name from products inner join category on a = category_id;
 s_no | product_name | category_name
------+--------------+---------------
    1 | 1kashayam    | kashayam
    2 | 1thailam     | thailam
    3 | 3lehyam      | lehyam
    4 | 2kashayam    | kashayam
    5 | 2thailam     | thailam
(5 rows)

INNER JOIN

some observations : 
In SQL, the INNER JOIN clause returns rows when there is a match in both tables. The order in which tables are specified in an INNER JOIN does not affect the result set, as long as the join condition remains the same.


query 1 : 
SELECT cust_id AS customer_id, cust_name AS customer_name, cut_email AS customer_email, amount AS "Payment Amount", p_id AS payment_id 
FROM customer 
INNER JOIN payments USING (cust_id);


query 2 : 
SELECT cust_id AS customer_id, cust_name AS customer_name, cut_email AS customer_email, amount AS "Payment Amount", p_id AS payment_id 
FROM payments 
INNER JOIN customer USING (cust_id);

Both queries will produce the same result because the INNER JOIN is commutative; that is, A INNER JOIN B is equivalent to B INNER JOIN A.


In SQL, the INNER JOIN clause returns rows when there is a match in both tables. The order in which tables are specified in an INNER JOIN does not affect the result set, as long as the join condition remains the same.

Let's take a look at the two queries and understand their results:

Query 1
sql
Copy code
SELECT cust_id AS customer_id, cust_name AS customer_name, cut_email AS customer_email, amount AS "Payment Amount", p_id AS payment_id 
FROM customer 
INNER JOIN payments USING (cust_id);
Query 2
sql
Copy code
SELECT cust_id AS customer_id, cust_name AS customer_name, cut_email AS customer_email, amount AS "Payment Amount", p_id AS payment_id 
FROM payments 
INNER JOIN customer USING (cust_id);

Both queries will produce the same result because the INNER JOIN is commutative; that is, A INNER JOIN B is equivalent to B INNER JOIN A.
   

Explanation
Interchanging the tables in the INNER JOIN clause does not change the output. The INNER JOIN operation will still join rows based on the matching cust_id from both tables.

The resulting table will contain all columns specified in the SELECT statement, where the join condition cust_id matches in both tables.

----------------------------------------------------------------------------------------------------------------


                                    GROUP BY

- It is important to note that The GROUP BY clause must exactly appear after the FROM or WHERE clause.