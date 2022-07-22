<div class="top">

# What tables with multi-row partitions are good for?
### [◂](command:katapod.loadPage?step10){.steps} Step 11 of 12 [▸](command:katapod.loadPage?step12){.steps}
</div>

In Cassandra, tables are designed to support specific queries. While tables with 
single-row partitions are usually used to store and retrieve entities,  
tables with multi-row partitions are great for capturing relationships.
For example, we used tables `ratings_by_user` and `ratings_by_movie` to store and query relationships like 
*user rated many movies* and its reverse *movie was rated by many users*, respectively.
Tables with multi-row partitions also have a greater flexibility in terms of how data
can be retrieved, which includes equality queries, inequality or range queries, 
and ordering queries.

Finally, tables with multi-row partitions are also suitable for storing entities related based on some attribute values,
such as *movies with the same title* in the example below. Of course, whether you need such a table in your data model or not
depends on whether you need to support queries that retrieve movies based on titles.
 
```
CREATE TABLE movies_by_title (
  title TEXT,
  year INT,
  duration INT,
  avg_rating FLOAT,
  PRIMARY KEY ((title), year)
) WITH CLUSTERING ORDER BY (year DESC);

INSERT INTO movies_by_title (title, year, duration, avg_rating) 
VALUES ('Alice in Wonderland', 2010, 108, 6.00);
INSERT INTO movies_by_title (title, year, duration, avg_rating) 
VALUES ('Alice in Wonderland', 1951, 75, 7.08);

SELECT * FROM movies_by_title
WHERE title = 'Alice in Wonderland';
```

[continue](command:katapod.loadPage?step12){.orange_bar}
