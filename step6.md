<div class="top">

# Create table "actors_by_movie"
### [◂](command:katapod.loadPage?step5){.steps} Step 6 of 12 [▸](command:katapod.loadPage?step7){.steps}
</div>

Our next table will store information about actors 
performing in movies, such that each partition will store all actors who 
performed in one particular movie. To define 
this table with *multi-row partitions*, we can use `title` and `year`, which uniquely identify a movie,
as a *composite partition key*, and `first_name` and `last_name`, which uniquely identify an actor, as a *composite clustering key*.
We will insert 3 rows into 2 partitions:

| title               | year | first_name       | last_name |
|---------------------|------|------------------|-----------|
| <span style="background-color:#F5B7B1">Alice in Wonderland</span> | <span style="background-color:#F5B7B1">2010</span> | Anne   | Hathaway |
| <span style="background-color:#F5B7B1">Alice in Wonderland</span> | <span style="background-color:#F5B7B1">2010</span> | Johnny | Depp     |
| <span style="background-color:#ABEBC6">Edward Scissorhands</span> | <span style="background-color:#ABEBC6">1990</span> | Johnny | Depp     |

This table is for you to create!

Create the table:
<details>
  <summary>Solution</summary>

```
CREATE TABLE actors_by_movie (
  title TEXT,
  year INT,
  first_name TEXT,
  last_name TEXT,
  PRIMARY KEY ((title, year), first_name, last_name)
);
```

</details>

Insert the rows:
<details>
  <summary>Solution</summary>

```
INSERT INTO actors_by_movie (title, year, first_name, last_name)  
VALUES ('Alice in Wonderland', 2010, 'Johnny', 'Depp');
INSERT INTO actors_by_movie (title, year, first_name, last_name) 
VALUES ('Alice in Wonderland', 2010, 'Anne', 'Hathaway');
INSERT INTO actors_by_movie (title, year, first_name, last_name)   
VALUES ('Edward Scissorhands', 1990, 'Johnny', 'Depp');
```

</details>

Q1. Retrieve one row:
<details>
  <summary>Solution</summary>

```
SELECT * FROM actors_by_movie
WHERE title = 'Alice in Wonderland'
  AND year = 2010
  AND first_name = 'Johnny'
  AND last_name = 'Depp';
```

</details>

Q2. Retrieve one partition:
<details>
  <summary>Solution</summary>

```
SELECT * FROM actors_by_movie
WHERE title = 'Alice in Wonderland'
  AND year = 2010;
```

</details>

Q3. Retrieve all rows:
<details>
  <summary>Solution</summary>

```
SELECT * FROM actors_by_movie;
```

</details>

[continue](command:katapod.loadPage?step7){.orange_bar}