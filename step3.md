<div class="top">

# Let's get started ...
### [◂](command:katapod.loadPage?step2){.steps} Step 3 of 12 [▸](command:katapod.loadPage?step4){.steps}
</div>

Start the CQL shell:
```
cqlsh
```

Create the keyspace:
```
CREATE KEYSPACE killr_video
WITH replication = {
  'class': 'NetworkTopologyStrategy', 
  'DC-Houston': 1 };
```

Set the current working keyspace:
```
USE killr_video;
```

[continue](command:katapod.loadPage?step4){.orange_bar}