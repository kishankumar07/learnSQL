-- This section will walks you through deleting a row from a table,



                             DELETE FROM fizz WHERE id=1;

**Make sure WHERE clause is there**




company=# select*from fizz;
 id | name  |      email      | gender | created_at
----+-------+-----------------+--------+------------
  1 | Arjun | arjun@gmail.com | M      | 2024-07-27
  2 | Raj   | raj@gmail.com   | M      | 2024-07-27
  3 | Rahul | rahul@gmail.com | M      | 2024-07-27
(3 rows)


company=# delete from fizz where id = 3;
DELETE 1
company=# select * from fizz;
 id | name  |      email      | gender | created_at
----+-------+-----------------+--------+------------
  1 | Arjun | arjun@gmail.com | M      | 2024-07-27
  2 | Raj   | raj@gmail.com   | M      | 2024-07-27
(2 rows)



----------------- be cautious to give not like this =========

                            DELETE FROM fizz;
this will empty your table !                


company=# delete from fizz;
 id | name  |      email      | gender | created_at
----+-------+-----------------+--------+------------
(0 rows)