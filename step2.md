<div class="top">

# Creating tables
### [◂](command:katapod.loadPage?step1){.steps} Step 2 of 12 [▸](command:katapod.loadPage?step3){.steps}
</div>

To create a table, Cassandra Query Language has the `CREATE TABLE` statement with the following simplified syntax:

<pre style="color: #a31516">
CREATE TABLE [ IF NOT EXISTS ] [keyspace_name.]table_name
( 
  column_name data_type [ , ... ] 
  PRIMARY KEY ( 
   ( partition_key_column_name  [ , ... ] )
   [ clustering_key_column_name [ , ... ] ]
  )     
)
[ WITH CLUSTERING ORDER BY 
   ( clustering_key_column_name ASC|DESC [ , ... ] )
];
</pre>

First, notice that a table is created within an existing keyspace. If a *keyspace name* is omitted, the current working keyspace is used.

Second, *keyspace*, *table* and *column* *names* can contain alphanumeric characters and underscores. By default, 
names are case-insensitive, but case sensitivity can be forced by using double quotation marks around a name.

Third, there are many CQL *data types*, including native, collection and user-defined data types. For now, we will use some of the simplest and 
self-descriptive ones like `TEXT`, `INT`, `FLOAT`, and `DATE`.

Fourth, notice that there are additional 
parentheses around the partition key columns that can be omitted when the partition key has only one column (a.k.a. 
*simple partition key*) and are required when the partition key has more than one column (a.k.a. 
*composite partition key*). 

Finally, when a clustering key is defined, ordering is optionally specified in the last clause with ascendant order being the default. 

[continue](command:katapod.loadPage?step3){.orange_bar}