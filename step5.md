<div class="top">

# Create table "ratings_by_movie"
### [◂](command:katapod.loadPage?step4){.steps} Step 5 of 12 [▸](command:katapod.loadPage?step6){.steps}
</div>

Our second table will store information about ratings 
organized by movies, such that each partition will store all ratings for one 
particular movie. To define 
this table with *multi-row partitions*, we can use `title` and `year`, which uniquely identify a movie, 
as a *composite partition key* and `email`, which uniquely identifies a user,
as a *simple clustering key*. We will insert 4 rows into 3 partitions:


| title               | year | email            | rating |
|---------------------|------|------------------|--------|
| <span style="background-color:#F5B7B1">Alice in Wonderland</span> | <span style="background-color:#F5B7B1">2010</span> | jen@datastax.com |     10 |
| <span style="background-color:#F5B7B1">Alice in Wonderland</span> | <span style="background-color:#F5B7B1">2010</span> | joe@datastax.com |      9 |
| <span style="background-color:#AED6F1">Alice in Wonderland</span> | <span style="background-color:#AED6F1">1951</span> | jen@datastax.com |      8 |
| <span style="background-color:#ABEBC6">Edward Scissorhands</span> | <span style="background-color:#ABEBC6">1990</span> | joe@datastax.com |     10 |


Create the table:
```
CREATE TABLE ratings_by_movie (
  title TEXT,
  year INT,
  email TEXT,
  rating INT,
  PRIMARY KEY ((title, year), email)
);
```

Insert the rows:
```
INSERT INTO ratings_by_movie (title, year, email, rating)  
VALUES ('Alice in Wonderland', 2010, 'jen@datastax.com', 10);
INSERT INTO ratings_by_movie (title, year, email, rating) 
VALUES ('Alice in Wonderland', 2010, 'joe@datastax.com', 9);
INSERT INTO ratings_by_movie (title, year, email, rating)   
VALUES ('Alice in Wonderland', 1951, 'jen@datastax.com', 8);
INSERT INTO ratings_by_movie (title, year, email, rating)   
VALUES ('Edward Scissorhands', 1990, 'joe@datastax.com', 10);
```

Q1. Retrieve one row:
```
SELECT * FROM ratings_by_movie
WHERE title = 'Alice in Wonderland'
  AND year = 2010
  AND email = 'joe@datastax.com';
```

Q2. Retrieve one partition:
```
SELECT * FROM ratings_by_movie
WHERE title = 'Alice in Wonderland'
  AND year = 2010;
```

Q3. Retrieve all rows:
```
SELECT * FROM ratings_by_movie;
```

[continue](command:katapod.loadPage?step6){.orange_bar}