<div dir="rtl">بنام خدا</div>

- [Installation Tips](#installation-tips)
  - [find Configuration](#find-configuration)
- [Users And Groups](#users-and-groups)
  - [Create user And Group](#creat-user-and-group)
  - [Set Permissions](#set-permissions)
- [Files And Directories Commands](#files-and-directories-commands)
  - [Create](#create)
  - [Delete](#delete)
  - [Read and Write](#read-and-write)
  - [Browse](#browse)
  - [Permissions](#permissions)
- [Tips](#tips)


[top](#top)
# Installation Tips
1- [this Link](https://www.tutorialspoint.com/hadoop/hadoop_multi_node_cluster.htm) and [this](https://linode.com/docs/databases/hadoop/how-to-install-and-set-up-hadoop-cluster/) are useful
2- be care on `chown user:group /hadoopName&Data Node Path` , which user will run hadoop command.
3- not forgot `jps` command to find the state of your hdfs.
4- `bin/hdfs dfsadmin -report` is useful.
5- if you need to format namenode, `hdfs namenode -format -clusterId CID-8bf63244-0510-4db6-a949-8f74b50f2be9` command may useful.
  - the clusterId is in /hdfsPath/namende/current/VERSION
  - that should be same with the same file in hadoop/tmp file which defined in _core-site.xml_ file.
  - the owner of hadoop should be able to _ssh passwordLess_ to __localhost__ .
  - I was needed to add below properties in config files due hive problems.
    ###### i. mapred-site.xml:
    ```xml
      <property>
        <name>mapred.reduce.tasks</name>
        <value>-1</value>
      </property>
      <property>
              <name>mapred.map.tasks</name>
              <value>-1</value>
      </property>
      <property>
              <name>mapreduce.job.reduces</name>
              <value>-1</value>
      </property>
      <property>
              <name>mapreduce.map.java.opts</name>
              <value>-Xmx1024M</value>
      </property>
      <property>
              <name>mapreduce.reduce.java.opts</name>
              <value>-Xmx2048M</value>
      </property>
    ```
    2. to increase mapred heap size:
    ```xml
      <property>
          <name>mapred.child.java.opts</name>
          <value>-Xmx4096m</value>
      </property>
    ```
### find configuration
```prolog
  hdfs getconf -confKey fs.defaultFS
```

[top](#top)
# Users And Groups
## Create user And Group
there is not any way to define to create user or group in hadoop till v.3, it used OS user and group.
only is below statement may use in _core-site.xml_ file:
```xml
    <property>
      <name>hadoop.proxyuser.hive.hosts</name>
      <value>*</value>
    </property>
    <property>
    <name>hadoop.proxyuser.hive.groups</name>
    <value>*</value>
    </property>
```

[top](#top)
# [Files And Directories Commands](#https://data-flair.training/blogs/top-hadoop-hdfs-commands-tutorial/)
## Create
### Create Folder
```prolog
  hdfs dfs -mkdir ...
```
## Delete
```prolog
  hdfs dfs -rm [-r] ...
  hdfs dfs -expunge   # empty trash
```
##  Read and Write
### Copy from local and vise versa
```prolog
  hdfs dfs -put|copyFromLocal|moveFromLocal localPath hdfsPath
  hdfs fs -get[merge]|copyTo|moveTo hdfsPath localPath
```
### Read
```prolog
  hdfs dfs -cat|tail [-f]| ...
```
## Browse
### Browse
```prolog
  hdfs dfs -ls [-R] ...
  hdfs dfs -mv|cp ... ...
```

## [Permissions](https://hadoop.apache.org/docs/r2.7.1/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)
- consider below commands:
- it has all linux Permission's commands:
```prolog
  hdfs dfs -chown|chmod|chgrp [-R] UserName:GroupName ...
  hdfs dfs -setfacl [Optrions One by One] u|g:Name|:Permission ...
  hdfs dfs -getfacl ...
  hdfs dfs -getfattr
```
  - please be aware for these properties:
    - first foe __core-site.xml__:
    ```xml
      <property>
        <name>dfs.permissions.enabled</name>
        <value>true</value>
      </property>
    ```
    - next for __hdfs-site.xml__:
    ```xml
      <property>
        <name>hadoop.tmp.dir</name>
        <value>/tmp/hadoop-$(user.name)</value>
      </property>
    ```

[top](#top)
# Tips
#### java.io.IOException: All directories in dfs.datanode.data.dir are invalid:
actually when I faced this error because I changed my hadoop version, according [this](https://stackoverflow.com/a/45094804/3214950) problem solved.



[top](#top)





