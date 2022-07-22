<div class="top">

# Create table "ratings_by_user"
### [◂](command:katapod.loadPage?step3){.steps} Step 4 of 12 [▸](command:katapod.loadPage?step5){.steps}
</div>

Our first table will store information about movie ratings 
organized by users, such that each partition will store all ratings left by one 
particular user. To define 
this table with *multi-row partitions*, we can use `email`, which uniquely identifies a user,
as a *simple partition key*, and `title` and `year`, which uniquely identify a movie, as a *composite clustering key*.
We will insert 4 rows into 2 partitions:

| email            | title               | year | rating |
|------------------|---------------------|------|--------|
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | Alice in Wonderland | 2010 |      9 |
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | Edward Scissorhands | 1990 |     10 |
| <span style="background-color:#AED6F1">jen@datastax.com</span> | Alice in Wonderland | 1951 |      8 |
| <span style="background-color:#AED6F1">jen@datastax.com</span> | Alice in Wonderland | 2010 |     10 |



Create the table:
```
CREATE TABLE ratings_by_user (
  email TEXT,
  title TEXT,
  year INT,
  rating INT,
  PRIMARY KEY ((email), title, year)
);
```

Insert the rows:
```
INSERT INTO ratings_by_user (email, title, year, rating) 
VALUES ('joe@datastax.com', 'Alice in Wonderland', 2010, 9);
INSERT INTO ratings_by_user (email, title, year, rating)  
VALUES ('joe@datastax.com', 'Edward Scissorhands', 1990, 10);
INSERT INTO ratings_by_user (email, title, year, rating) 
VALUES ('jen@datastax.com', 'Alice in Wonderland', 2010, 10);
INSERT INTO ratings_by_user (email, title, year, rating)  
VALUES ('jen@datastax.com', 'Alice in Wonderland', 1951, 8);
```

Q1. Retrieve one row:
```
SELECT * FROM ratings_by_user
WHERE email = 'joe@datastax.com'
  AND title = 'Alice in Wonderland'
  AND year = 2010;
```

Q2. Retrieve one partition:
```
SELECT * FROM ratings_by_user
WHERE email = 'joe@datastax.com';
```

Q3. Retrieve all rows:
```
SELECT * FROM ratings_by_user;
```

[continue](command:katapod.loadPage?step5){.orange_bar}