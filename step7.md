<div class="top">

# Create table "movies_by_actor"
### [◂](command:katapod.loadPage?step6){.steps} Step 7 of 12 [▸](command:katapod.loadPage?step8){.steps}
</div>

Next, we can design another table to store the inverse relationship of movies by actors, 
such that each partition will store all movies where a given actor performed. To define 
this table with *multi-row partitions*, we can use `first_name` and `last_name`, which uniquely identify an actor,
as a *composite partition key*, and `title` and `year`, which uniquely identify a movie, as a *composite clustering key*.
We will insert 3 rows into 2 partitions:

| first_name | last_name | title               | year |
|------------|-----------|---------------------|------|
|     <span style="background-color:#F5B7B1">Johnny</span> |  <span style="background-color:#F5B7B1">    Depp</span> | Alice in Wonderland | 2010 |
|     <span style="background-color:#F5B7B1">Johnny</span> |  <span style="background-color:#F5B7B1">    Depp</span> | Edward Scissorhands | 1990 |
|     <span style="background-color:#ABEBC6">  Anne</span> |  <span style="background-color:#ABEBC6">Hathaway</span> | Alice in Wonderland | 2010 |

This table is for you to create!

Create the table:
<details>
  <summary>Solution</summary>

```
CREATE TABLE movies_by_actor (
  first_name TEXT,
  last_name TEXT,
  title TEXT,
  year INT,  
  PRIMARY KEY ((first_name, last_name), title, year)
);
```

</details>

Insert the rows:
<details>
  <summary>Solution</summary>

```
INSERT INTO movies_by_actor (first_name, last_name, title, year)  
VALUES ('Johnny', 'Depp', 'Alice in Wonderland', 2010);
INSERT INTO movies_by_actor (first_name, last_name, title, year)   
VALUES ('Johnny', 'Depp', 'Edward Scissorhands', 1990);
INSERT INTO movies_by_actor (first_name, last_name, title, year)
VALUES ('Anne', 'Hathaway', 'Alice in Wonderland', 2010);
```

</details>

Q1. Retrieve one row:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies_by_actor
WHERE first_name = 'Johnny'
  AND last_name = 'Depp'
  AND title = 'Alice in Wonderland'
  AND year = 2010;
```

</details>

Q2. Retrieve one partition:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies_by_actor
WHERE first_name = 'Johnny'
  AND last_name = 'Depp';
```

</details>

Q3. Retrieve all rows:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies_by_actor;
```

</details>

[continue](command:katapod.loadPage?step8){.orange_bar}
