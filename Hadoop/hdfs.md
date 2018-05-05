<div dir="rtl">بنام خدا</div>

- [Installation Tips](#installation-tips)
- [Commands](#commands)
  - [Create Write Read Delete File and Directory](#create-write-read-delete-file-and-directory)
- [Tips](#tips)


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
# Create Write Read Delete File and Directory
### Copy from local and vise versa
```vala
  hadoop fs -put localPath hdfsPath
  hadoop fs -copyFromLocal localPath hdfsPath
  hadoop fs -get hdfsPath localPath
```


[top](#top)

# Tips
#### java.io.IOException: All directories in dfs.datanode.data.dir are invalid:
actually when I faced this error because I changed my hadoop version, according [this](https://stackoverflow.com/a/45094804/3214950) problem solved.



[top](#top)






