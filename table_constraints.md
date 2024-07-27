- constraints can be created when table creation time and after table creation time.

case 1) lets see how to do this while table creation:

Here is a sample table creation ; 


                                CREATE TABLE bottles(
                                    id INT PRIMARY KEY,
                                    name VARCHAR(100) NOT NULL,
                                    email VARCHAR(100) NOT NULL UNIQUE,
                                    gender CHECK (gender = 'M' OR gender = 'F'),
                                    created_at DATE DEFAULT CURRENT_TIMESTAMP
                                );


company=# drop table jack;
DROP TABLE
company=# create table bottles(
company(# id int primary key,
company(# name varchar(100) not null,
company(# email varchar(100) not null unique,
company(# gender varchar(10) check (gender='M' or gender='F'),
company(# created_at date default current_timestamp);
CREATE TABLE
company=# \d bottles
                             Table "public.bottles"
   Column   |          Type          | Collation | Nullable |      Default
------------+------------------------+-----------+----------+-------------------
 id         | integer                |           | not null |
 name       | character varying(100) |           | not null |
 email      | character varying(100) |           | not null |
 gender     | character varying(10)  |           |          |
 created_at | date                   |           |          | CURRENT_TIMESTAMP
Indexes:
    "bottles_pkey" PRIMARY KEY, btree (id)
    "bottles_email_key" UNIQUE CONSTRAINT, btree (email)
Check constraints:
    "bottles_gender_check" CHECK (gender::text = 'M'::text OR gender::text = 'F'::text)




---------------------------------------------------------------------------------------------------------------

case 2 : after creating table entering the constaints :

                            CREATE TABLE bottles(
                                id int,
                                name varchar(100),
                                email varchar(100),
                                gender varchar(10),
                                created_at date default current_timestamp
                            );

company=# \d bottles
                             Table "public.bottles"
   Column   |          Type          | Collation | Nullable |      Default
------------+------------------------+-----------+----------+-------------------
 id         | integer                |           |          |
 name       | character varying(100) |           |          |
 email      | character varying(100) |           |          |
 gender     | character varying(10)  |           |          |
 created_at | date                   |           |          | CURRENT_TIMESTAMP




So now the table is created , 
1) Going to make id as primary key:

                    ALTER TABLE bottles ADD CONSTRAINT bottles_pkey PRIMARY KEY (id);

company=# alter table bottles add constraint bottles_pkey primary key(id);
ALTER TABLE
company=# \d bottles
                             Table "public.bottles"
   Column   |          Type          | Collation | Nullable |      Default
------------+------------------------+-----------+----------+-------------------
 id         | integer                |           | not null |
 name       | character varying(100) |           |          |
 email      | character varying(100) |           |          |
 gender     | character varying(10)  |           |          |
 created_at | date                   |           |          | CURRENT_TIMESTAMP
Indexes:
    "bottles_pkey" PRIMARY KEY, btree (id)


Now we see that id is a primary key now, and "NOT NULL" came automatically see above,.

2) Going to set name and emai as NOT NULL :

                    ALTER TABLE bottles ALTER COLUMN email SET NOT NULL;

3)                  ALTER TABLE bottles ALTER COLUMN name SET NOT NULL;

                                           ^
company=# alter table bottles alter column email set not null;
ALTER TABLE
company=# \d bottles;
                             Table "public.bottles"
   Column   |          Type          | Collation | Nullable |      Default
------------+------------------------+-----------+----------+-------------------
 id         | integer                |           | not null |
 name       | character varying(100) |           | not null |
 email      | character varying(100) |           | not null |
 gender     | character varying(10)  |           |          |
 created_at | date                   |           |          | CURRENT_TIMESTAMP
Indexes:
    "bottles_pkey" PRIMARY KEY, btree (id)



4)Make email as UNIQUE :


                    ALTER TABLE bottles ADD CONSTRAINT bottles_unique_email UNIQUE (email);


company=# alter table bottles add constraint bottles_unique_email unique (email);
ALTER TABLE
company=# \d bottles
                             Table "public.bottles"
   Column   |          Type          | Collation | Nullable |      Default
------------+------------------------+-----------+----------+-------------------
 id         | integer                |           | not null |
 name       | character varying(100) |           | not null |
 email      | character varying(100) |           | not null |
 gender     | character varying(10)  |           |          |
 created_at | date                   |           |          | CURRENT_TIMESTAMP
Indexes:
    "bottles_pkey" PRIMARY KEY, btree (id)
    "bottles_unique_email" UNIQUE CONSTRAINT, btree (email)



5) apply gender CHECK to gender:


            ALTER TABLE bottles ADD CONSTRAINT bottles_gender_check CHECK (gender IN ('M','F'));


company=# alter table bottles add constraint bottles_gender_check CHECK (gender in ('M','F'));
ALTER TABLE
company=# \d bottles
                             Table "public.bottles"
   Column   |          Type          | Collation | Nullable |      Default
------------+------------------------+-----------+----------+-------------------
 id         | integer                |           | not null |
 name       | character varying(100) |           | not null |
 email      | character varying(100) |           | not null |
 gender     | character varying(10)  |           |          |
 created_at | date                   |           |          | CURRENT_TIMESTAMP
Indexes:
    "bottles_pkey" PRIMARY KEY, btree (id)
    "bottles_unique_email" UNIQUE CONSTRAINT, btree (email)
Check constraints:
    "bottles_gender_check" CHECK (gender::text = ANY (ARRAY['M'::character varying, 'F'::character varying]::text[]))




6) now add DEFAULT to created_at :


            ALTER TABLE bottles ALTER COLUMN created_at SET DEFAULT current_timestamp;


company=# alter table bottles alter column created_at SET DEFAULT current_timestamp;
ALTER TABLE
company=# \d bottles
                             Table "public.bottles"
   Column   |          Type          | Collation | Nullable |      Default
------------+------------------------+-----------+----------+-------------------
 id         | integer                |           | not null |
 name       | character varying(100) |           | not null |
 email      | character varying(100) |           | not null |
 gender     | character varying(10)  |           |          |
 created_at | date                   |           |          | CURRENT_TIMESTAMP
Indexes:
    "bottles_pkey" PRIMARY KEY, btree (id)
    "bottles_unique_email" UNIQUE CONSTRAINT, btree (email)
Check constraints:
    "bottles_gender_check" CHECK (gender::text = ANY (ARRAY['M'::character varying, 'F'::character varying]::text[]))






------------ Once you reach here you have created a table ------------------


----------- If while table creation is constraints not given ,no worries still you can add it even after by following the steps above