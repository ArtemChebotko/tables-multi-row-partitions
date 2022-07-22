<div class="top">

# Tables, columns, data types, rows, partitions, keys, ordering
### [◂](command:katapod.loadPage?intro){.steps} Step 1 of 12 [▸](command:katapod.loadPage?step2){.steps}
</div>

A *table* in Apache Cassandra™ shares many similarities with a table in a relational database. It has named *columns* with *data types* and *rows* with *values*. A *primary key* uniquely identifies a row in a table. 

There are also important differences. In Cassandra, on one hand, a table is a set of *rows* containing values and, on the other hand,
a table is also a set of *partitions* containing rows. Specifically, each row belongs to exactly one partition and each partition contains 
one or more rows. A *primary key* consists of a mandatory *partition key* and optional *clustering key*, where
a partition key uniquely identifies a partition in a table and a clustering key uniquely identifies a row in a partition.

A table with *single-row partitions* is a table where there is exactly one row per partition. A table 
with single-row partitions defines a primary key to be equivalent to a partition key.  

A table with *multi-row partitions* is a table where there can be one or more rows per partition. A table 
with multi-row partitions defines a primary key to be a combination of both partition and clustering keys. Rows in the 
same partition have the same partition key values and are *ordered* based on their clustering key values using the default ascendant order.

[continue](command:katapod.loadPage?step2){.orange_bar}