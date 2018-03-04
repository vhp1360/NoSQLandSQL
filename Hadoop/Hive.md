<div dir="rtl">بنام خدا</div>


Hive installation:

1. [edureka Link](https://www.edureka.co/blog/apache-hive-installation-on-ubuntu) is good
2. be careful on metastore issue:
  - Hive and metastore version consistency
  - User Permission Issue
  - in metastore issue use _verbose_ to more log : `bin/schematool -initSchema -dbType derby --verbose`
  - still you need `hive-site.xml` file
  - be care to where _derby.db_ file and _metastore\_db_ drive crreate
3. the log file will stored in /tmp/UserName/hive.log































































[top](#top)
