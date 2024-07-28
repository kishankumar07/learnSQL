- This will lets you know how to upsert a row during conflict

- Normally if you try to violate any constraint, it throws an error, so inorder to avoid that there are two ways:

- Either 
1) DO NOTHING ;
2) DO UPDATE ;


Let's see that with an example :


                            SELECT * FROM fizz;

company=# select*from fizz;
 id | name  |      email      | gender | created_at
----+-------+-----------------+--------+------------
  1 | John  | john@gmail.com  | M      | 2024-07-28
  2 | Rahul | rahul@gmail.com | M      | 2024-07-28
(2 rows)


company=# insert into fizz(id,name,email,gender)
company-# values(2,'Sam','sam@gmail.com','M');
ERROR:  duplicate key value violates unique constraint "fizz_pkey"
DETAIL:  Key (id)=(2) already exists.
company=#


see above that , to the same primary key of 2 , I again tries to add a field , so the error message comes as above,

1)

lets now deal with DO NOTHING :

                INSERT INTO fizz(id,name,email,gender) VALUES (2,'Roju','roju@gmail.com','M')

                ON CONFLICT (id) DO NOTHING

company=# insert into fizz(id,name,email,gender) values(2,'Roju','roju@gmail.com','M')
company-# on conflict (id) do nothing;
INSERT 0 0

nothing got happened !


2)

Let's see how DO UPDATE goes instead of DO NOTHING.

                SELECT * FROM fizz;

company=# select * from fizz;
 id | name |     email      | gender | created_at
----+------+----------------+--------+------------
  1 | John | john@gmail.com | M      | 2024-07-28
  2 | Alex | alex@gmail.com | M      | 2024-07-28
(2 rows)


                INSERT INTO fizz(id,name,email,gender) VALUES (2,'Raju','raju@gmail.com','M')

                ON CONFLICT (id) DO UPDATE name = EXCLUDED.name,email = EXCLUDED.email;

company=# insert into fizz(id,name,email,gender) values (2,'Raju','raju@gmail.com','M')
company-# on conflict (id) do update set name = excluded.name,email = excluded.email;
INSERT 0 1
company=# select*from fizz;
 id | name |     email      | gender | created_at
----+------+----------------+--------+------------
  1 | John | john@gmail.com | M      | 2024-07-28
  2 | Raju | raju@gmail.com | M      | 2024-07-28
(2 rows)



------------- With this you learned how to handle conflict using 2 cases, either ignore that insert or upsert it=----------------