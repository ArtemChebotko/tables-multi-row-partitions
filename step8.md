<div class="top">

# Clustering order
### [◂](command:katapod.loadPage?step7){.steps} Step 8 of 12 [▸](command:katapod.loadPage?step9){.steps}
</div>

Besides serving as a unique row identifier within a partition, a clustering key also defines
how rows are ordered within the same partition. In case of a composite clustering key,
rows are first ordered by the first clustering key column, then the second one and so forth. It 
should now be evident that `PRIMARY KEY ((email), title, year)` and `PRIMARY KEY ((email), year, title)`
are not the same. The clustering order affects both storage and retrieval, including efficient range queries on clustering key 
columns. Rows are always retrieved using the clustering order or its reverse.
While the default order for each column is ascendant or `ASC`, it can be customized on a per column basis
using the `CLUSTERING ORDER BY` clause. Check out the following example.

Drop the existing table:
```
DROP TABLE IF EXISTS ratings_by_user;
```

Create the new table:
```
CREATE TABLE ratings_by_user (
  email TEXT,
  year INT,
  title TEXT,
  rating INT,
  PRIMARY KEY ((email), year, title)
) WITH CLUSTERING ORDER BY (year DESC, title ASC);
```

Insert the rows:
```
INSERT INTO ratings_by_user (email, year, title, rating) 
VALUES ('joe@datastax.com', 2010, 'Despicable Me', 5);
INSERT INTO ratings_by_user (email, year, title, rating) 
VALUES ('joe@datastax.com', 2010, 'Toy Story 3', 10);
INSERT INTO ratings_by_user (email, year, title, rating) 
VALUES ('joe@datastax.com', 1951, 'Alice in Wonderland', 7);
INSERT INTO ratings_by_user (email, year, title, rating) 
VALUES ('joe@datastax.com', 2010, 'Alice in Wonderland', 9);
INSERT INTO ratings_by_user (email, year, title, rating) 
VALUES ('joe@datastax.com', 1990, 'Edward Scissorhands', 10);
INSERT INTO ratings_by_user (email, year, title, rating) 
VALUES ('jen@datastax.com', 2010, 'Alice in Wonderland', 10);
```

Q1. Retrieve one partition:
```
SELECT * FROM ratings_by_user
WHERE email = 'joe@datastax.com';
```

Q2. Retrieve one partition using the reverse row ordering:
```
SELECT * FROM ratings_by_user
WHERE email = 'joe@datastax.com'
ORDER BY year ASC, title DESC;
```

Q3. Retrieve a subset of rows from one partition:
```
SELECT * FROM ratings_by_user
WHERE email = 'joe@datastax.com'
  AND year < 2000;
```

[continue](command:katapod.loadPage?step9){.orange_bar}
