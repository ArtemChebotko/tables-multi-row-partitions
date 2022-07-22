<div class="top">

# Static columns
### [◂](command:katapod.loadPage?step9){.steps} Step 10 of 12 [▸](command:katapod.loadPage?step11){.steps}
</div>

Some non-key columns in a table with *multi-row partitions* can be declared 
as *static columns*. A *static column* is shared by all rows belonging to 
the same partition. Therefore, if you know that a partition key functionally determines 
a non-key column in a table with multi-row partitions, then the non-key column will always have the 
same value for any row in a partition and should be declared *static* to optimize 
the storage and simplify column updates.

A static column is defined within the `CREATE TABLE` statement using the `STATIC` keyword, 
which we purposefully omitted in our previous discussions for simplicity.

Let's re-design table `ratings_by_user` to store not only movie ratings organized by users,
but also user names and ages as shown in the example below. Notice that `email`, `name`, and `age`
are all attributes or descriptors of users. Moreover, `email` unique identifies both a user and a partition in
the table, such that any row in the same partition will have the same `name` and `age`.

| email            | title               | year | rating | name | age |
|------------------|---------------------|------|--------|------|-----|
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | Alice in Wonderland | 2010 |      9 | <span style="background-color:#FDEDEC">Joe</span> | <span style="background-color:#FDEDEC">25</span> |
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | Edward Scissorhands | 1990 |     10 | <span style="background-color:#FDEDEC">Joe</span> | <span style="background-color:#FDEDEC">25</span> |
| <span style="background-color:#AED6F1">jen@datastax.com</span> | Alice in Wonderland | 1951 |      8 | <span style="background-color:#EBF5FB">Jen</span> | <span style="background-color:#EBF5FB">27</span> |
| <span style="background-color:#AED6F1">jen@datastax.com</span> | Alice in Wonderland | 2010 |     10 | <span style="background-color:#EBF5FB">Jen</span> | <span style="background-color:#EBF5FB">27</span> |

Drop the existing table:
```
DROP TABLE IF EXISTS ratings_by_user;
```

Create the new table:
```
CREATE TABLE ratings_by_user (
  email TEXT,
  title TEXT,
  year INT,
  rating INT,
  name TEXT STATIC,
  age INT STATIC,
  PRIMARY KEY ((email), title, year)
);
```

Insert the rows:
```
INSERT INTO ratings_by_user (email, title, year, rating, name, age) 
VALUES ('joe@datastax.com', 'Alice in Wonderland', 2010, 9, 'Joe', 25);
INSERT INTO ratings_by_user (email, title, year, rating, name, age) 
VALUES ('joe@datastax.com', 'Edward Scissorhands', 1990, 10, 'Joe', 25);
INSERT INTO ratings_by_user (email, title, year, rating, name, age)
VALUES ('jen@datastax.com', 'Alice in Wonderland', 2010, 10, 'Jen', 27);
INSERT INTO ratings_by_user (email, title, year, rating, name, age)
VALUES ('jen@datastax.com', 'Alice in Wonderland', 1951, 8, 'Jen', 27);
```

Verify the result:
```
SELECT * FROM ratings_by_user;
```

Update static columns:
```
UPDATE ratings_by_user SET name = 'Joseph' 
WHERE email = 'joe@datastax.com';
UPDATE ratings_by_user SET age = 28 
WHERE email = 'jen@datastax.com';
```

Verify the result:
```
SELECT * FROM ratings_by_user;
```

[continue](command:katapod.loadPage?step11){.orange_bar}
