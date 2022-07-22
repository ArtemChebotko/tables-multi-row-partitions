<div class="top">

# Create table "movies_by_user"
### [◂](command:katapod.loadPage?step8){.steps} Step 9 of 12 [▸](command:katapod.loadPage?step10){.steps}
</div>

This next table will store information about movies that users watched, 
such that each partition will store all movies for one particular user 
ordered by the dates of when the user watched them. Here are 6 rows to be inserted into 2 partitions:

| email            | watched_on | title               | year |
|------------------|------------|---------------------|------|
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | 2020-04-28 | Edward Scissorhands | 1990 |
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | 2020-03-08 | Alice in Wonderland | 2010 | 
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | 2020-02-13 |         Toy Story 3 | 2010 |
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | 2020-01-22 |       Despicable Me | 2010 |
| <span style="background-color:#F5B7B1">joe@datastax.com</span> | 2019-12-30 | Alice in Wonderland | 1951 |
| <span style="background-color:#ABEBC6">jen@datastax.com</span> | 2011-10-01 | Alice in Wonderland | 2010 |


This table is for you to create!

Create the table:
<details>
  <summary>Solution</summary>

```
CREATE TABLE movies_by_user (
  email TEXT,
  title TEXT,
  year INT,
  watched_on DATE,
  PRIMARY KEY ((email), watched_on, title, year)
) WITH CLUSTERING ORDER BY (watched_on DESC);
```

</details>

Insert the rows:
<details>
  <summary>Solution</summary>

```
INSERT INTO movies_by_user (email, watched_on, title, year) 
VALUES ('joe@datastax.com', '2020-01-22', 'Despicable Me', 2010);
INSERT INTO movies_by_user (email, watched_on, title, year) 
VALUES ('joe@datastax.com', '2020-02-13', 'Toy Story 3', 2010);
INSERT INTO movies_by_user (email, watched_on, title, year) 
VALUES ('joe@datastax.com', '2019-12-30', 'Alice in Wonderland', 1951);
INSERT INTO movies_by_user (email, watched_on, title, year) 
VALUES ('joe@datastax.com', '2020-03-08', 'Alice in Wonderland', 2010);
INSERT INTO movies_by_user (email, watched_on, title, year) 
VALUES ('joe@datastax.com', '2020-04-28', 'Edward Scissorhands', 1990);
INSERT INTO movies_by_user (email, watched_on, title, year) 
VALUES ('jen@datastax.com', '2011-10-01', 'Alice in Wonderland', 2010);
```

</details>

Q1. Retrieve one partition:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies_by_user
WHERE email = 'joe@datastax.com';
```

</details>

Q2. Retrieve one partition using the reverse row ordering:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies_by_user
WHERE email = 'joe@datastax.com'
ORDER BY watched_on ASC;
```

</details>

Q3. Retrieve a subset of rows from one partition:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies_by_user
WHERE email = 'joe@datastax.com'
  AND watched_on > '2020-01-01';
```

</details>

[continue](command:katapod.loadPage?step10){.orange_bar}
