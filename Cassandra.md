<div dir=rtl>بنام خدا</div>

- [Keyspace](#keyspace)




### Keyspace
- Create:
```vala
  CREATE KEYSPACE KetSpaceName WITH replication= {'class': 'SimpleStrategy','replication_factor' : 3};
  CREATE KEYSPACE KetSpaceName WITH replication= {'class': 'NetworkTopologyStrategy','DC1' : 1,'DC2' : 3}
            AND durable_writes = false;
```
- Alter:
```vala
  ALTER KEYSPACE KetSpaceName WITH replication = {'class': 'SimpleStrategy', 'replication_factor' : 4};
```
- Drop:
```vala
  CDROP KEYSPACE KetSpaceName;
```
- Qury:
```vala
  DESCRIBE keyspaces;
```
  
### Table
- Create
  1. synopsis
  ```vala
    create_table_statement ::=  CREATE TABLE [ IF NOT EXISTS ] table_name
                              '('
                                  column_definition
                                  ( ',' column_definition )*
                                  [ ',' PRIMARY KEY '(' primary_key ')' ]
                              ')' [ WITH table_options ]

    column_definition      ::=  column_name cql_type [ STATIC ] [ PRIMARY KEY]

    primary_key            ::=  partition_key [ ',' clustering_columns ]

    partition_key          ::=  column_name
                              | '(' column_name ( ',' column_name )* ')'

    clustering_columns     ::=  column_name ( ',' column_name )*

    table_options          ::=  COMPACT STORAGE [ AND table_options ]
                              | CLUSTERING ORDER BY '(' clustering_order ')' [ AND table_options ]
                              | options

    clustering_order       ::=  column_name (ASC | DESC) ( ',' column_name (ASC | DESC) )*
  ```
  2. Example:
  ```vala
    CREATE TABLE TableName (
        species text PRIMARY KEY,
        common_name text,
        population varint,
        average_size int[,]
        PRIMARY KEY ((machine, cpu), mtime)
    ) WITH comment='Important biological records'
       AND read_repair_chance = 1.0
       AND compaction = { 'class' : 'LeveledCompactionStrategy' }
       AND CLUSTERING ORDER BY (mtime DESC);
```
3. Some types:
  _text_,_varchar_,_int_,_tinyint_,bigint_,

   
   
  
  
  
