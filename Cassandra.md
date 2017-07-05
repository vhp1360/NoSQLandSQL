<div dir=rtl>بنام خدا</div>

- [Keyspace](#keyspace)





### Keyspace
- Create:
```vala
  CREATE KEYSPACE Excelsior WITH replication = {'class': 'SimpleStrategy', 'replication_factor' : 3};
  CREATE KEYSPACE Excalibur WITH replication = {'class': 'NetworkTopologyStrategy', 'DC1' : 1, 'DC2' : 3}
            AND durable_writes = false;
```

