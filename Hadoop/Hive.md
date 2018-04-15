<div dir="rtl">بنام خدا</div>

- [Hive installation](#hive-installation)
  - [Install with Derby](#install-with-derby)
  - [Install with MySQL](#install-with-mysql)
- [Loading Csv](#loading-csv)
- [Sql Commands](#sql-commands)
- [Tips](#tips)

# Hive installation:

### Install with derby
by [this](https://cwiki.apache.org/confluence/display/Hive/HiveDerbyServerMode) or [this](http://thompsonng.blogspot.fr/2017/01/hadoop-installing-hive-with-derby.html)
- after installation becare on _${system:java.io.tmpdir}_ in __hive-site.xml__ file and may need to change it.
- also 
```hive
  schematool -initSchema -dbType derby
```
- if you faced _FAILED: SemanticException org.apache.hadoop.hive.ql.metadata.HiveException: \
    java.lang.RuntimeException: Unable to instantiate org.apache.hadoop.hive.ql.metadata.SessionHiveMetaStoreClient_ \
    by running `show tables;` To fix that `rm -Rf metastore_db` also [find this guid](https://stackoverflow.com/questions/43947930/unable-to-initialize-hive-with-derby-from-brew-install)
###### - to run it as service:
 ```vala
  nohup startNetworkServer -h 0.0.0.0 > /var/log/derby.log & 
  nohup /Path/2/hive/bin/hive --service hiveserver2 > /var/log/hiveserver2.log &
```

### Install with MySQL
1. [edureka Link](https://www.edureka.co/blog/apache-hive-installation-on-ubuntu) is good
2. be careful on metastore issue:
  - Hive and metastore version consistency
  - User Permission Issue
  - in metastore issue use _verbose_ to more log : `bin/schematool -initSchema -dbType derby --verbose`
  - still you need `hive-site.xml` file
  - be care to where _derby.db_ file and _metastore\_db_ drive crreate
3. the log file will stored in /tmp/UserName/hive.log

[top](#top)

# Loading Csv
- [one way](http://www.informit.com/articles/article.aspx?p=2756471&seqNum=4):
```vala
  CREATE EXTERNAL TABLE IF NOT EXISTS Names(Field1 INT,Field2 STRING,Field3 DATE,...)
    COMMENT 'Table Comment' ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' STORED AS TEXTFILE
    LOCATION '/Path/2/CSV';
```
- another way:
```vala
  CREATE TABLE TableName (...) row format delimited fields terminated by ',';
  LOAD DATA LOCAL INPATH '/home/yourcsvfile.csv' OVERWRITE INTO TABLE TableName;
```
  - in loading for Int column I faced Null in first record Result, for this use [tblproperties ("skip.header.line.count"="1")](https://stackoverflow.com/questions/43631472/how-i-avoid-the-null-in-the-first-field-name-of-hive-table)
  - to show column name in query: `hive>set hive.cli.print.header=true;`
  

[top](#top)

# Sql Commands
- Meta Data:
```sql
  show tables;
  alter table TblName rename to NewName;
  
```
- Query:
```sql

```

[top](#top)

# Tips
##### First: 
hive log return is awful, there is a web gui with hiveserver2 on 10002 port.
##### Second:
hive could run on top of some kind of engine:
  - mapreduce
  - spark
  - ant
  - tez : this is hadoop suggestion.
  
- if you encountered that _User1 could not impersonated User2_ from __Hive__ then
  1- change _false_ to _true_ for _hive.metastore.sasl.enabled_ property in _hive-site.xml_ file.
  2- add below in _core-site.xml_ in your hadoop:
  ```xml
    <property>
         <name>hadoop.proxyuser.server.hosts</name> 
         <value>*</value> 
    </property> 
    <property>
         <name>hadoop.proxyuser.server.groups</name>
         <value>*</value>
    </property>
  ```
- In _java.lang.RuntimeException:Unable to instantiate org.apache.hadoop.hive.metastore.HiveMetaStoreClient_ error and the solution [is](https://stackoverflow.com/questions/22711364/java-lang-runtimeexceptionunable-to-instantiate-org-apache-hadoop-hive-metastor) `rm   metastore_db/*.lck`
  - in this case you should first stop services, delete issues [then run it](to-run-it-as-service)
- in complicated queries I faced _FAILED: Execution Error, return code 2 from org.apache.hadoop.hive.ql.exec.mr.MapRedTask_ error, for that:
  1- added [this config in hadoop](https://github.com/vhp1360/NoSQLandSQL/blob/master/Hadoop/hdfs.md#1-mapred-sitexml)
  2- set `hive.exec.reducers.bytes.per.reducer` value in hive-site.xml to _1000000_ .
  3- [finally](https://stackoverflow.com/questions/8762064/hive-unable-to-manually-set-number-of-reducers) below configs solved my problem:
  ```vala
    set mapred.reduce.tasks=50;
    set mapred.map.tasks=50;
  ```
  
- [_5 WAYS TO MAKE YOUR HIVE QUERIES RUN FASTE_](https://hortonworks.com/blog/5-ways-make-hive-queries-run-faster/) is useful documnet.

[top](#top)

