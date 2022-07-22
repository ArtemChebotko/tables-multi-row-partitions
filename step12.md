<div class="top">

# Working with tables
### [◂](command:katapod.loadPage?step11){.steps} Step 12 of 12 [▸](command:katapod.loadPage?step13){.steps}
</div>

Try the following CQL shell commands and CQL statements that are applicable to tables. 

1. List the names of all tables in the current keyspace:
```
DESCRIBE TABLES;
```

2. Output all CQL statements that can be used to recreate the given table:
```
DESCRIBE TABLE ratings_by_user;
```

3. Alter the given table:
```
ALTER TABLE ratings_by_user DROP age;
```

4. Delete all rows from the table:
```
TRUNCATE ratings_by_user;
```

5. Remove the given table:
```
DROP TABLE ratings_by_user;
```

[continue](command:katapod.loadPage?finish){.orange_bar}
