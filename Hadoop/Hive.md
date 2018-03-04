<div dir="rtl">بنام خدا</div>

-[Hive installation](#hive-installation)
  - [Install with Derby](#install-with-derby)
  - [Install with MySQL](#install-with-mysql)
  
-[Loading Csv](#loading-csv)

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

[top](#top)
