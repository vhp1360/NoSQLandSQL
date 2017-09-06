<div dir=rtl>بنام خدا</div>

1- Totlay:
```bash
  createdb testdb
  psql testdb
  psql -U [username]
```  

2-DB
```psql
  \help <command_name>
  \c database_name; -> Change DataBase
  \l -> List All DataBases
  \dn -> List All Schemas
  \d{n,u,t,f,v} -> List All {Schemas, Users, Tables, StoreProcedures, Views}
  \x -> Show query in pretty format
  \{t,f}+ {table,function}_name -> detail of ...
  CREATE ROLE Role_Name;
  CREATE ROLE NOINHERIT LOGIN PASSWORD Passwoed;
  CREATE DATABASE [IF NOT EXISTS] DBName;
  DROP DATABASE DBName;
```
3-Table
```psql
  CREATE [TEMP] TABLE [IF NOT EXISTS] table_name(
    pk SERIAL PRIMARY KEY,
    c1 type(size) NOT NULL,
    c2 type(size) NULL,
    ...
  );
  ALTER TABLE table_name ADD COLUMN new_column_name TYPE;
  ALTER TABLE table_name DROP COLUMN column_name;
  ALTER TABLE table_name RENAME column_name TO new_column_name;
  ALTER TABLE table_name ALTER COLUMN [SET DEFAULT value | DROP DEFAULT]
  ALTER TABLE table_name ADD PRIMARY KEY (column,...);
  ALTER TABLE table_name 
  DROP CONSTRAINT primary_key_constraint_name;
  ALTER TABLE table_name RENAME TO new_table_name;
  DROP TABLE [IF EXISTS] table_name CASCADE;
```
4- View
```psql
  CREATE OR REPLACE view_name AS query;
  CREATE RECURSIVE VIEW view_name(columns) AS SELECT columns;
  CREATE MATERIALIZED VIEW view_name AS query WITH [NO] DATA;
  DROP VIEW [ IF EXISTS ] view_name;
  ALTER VIEW view_name RENAME TO new_name;
```
5- Index
```psql
  CREATE [UNIQUE] INDEX index_name ON table (column,...);
  DROP INDEX index_name;
```
6- Query
```psql
  SELECT * FROM table_name WHERE column IN (value1, value2,...) LIMIT limit OFFSET offset ORDER BY column_name;
  SELECT * FROM table1 {INNER,LEFT,FULL[ OUTER],CROSS,NATURAL} JOIN table2 ON conditions;
  SELECT * FROM table1 {UNION,EXCEPT,INTERSECT} SELECT * FROM table2;
```




















