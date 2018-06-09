<div dir=rtl>بنام خدا</div>

- [Thrift Server](#thrift-server)
- [Tips](#tips)


[top](#top)
# Thrif Server
my experience:
  1. first we need hadoop and spark distributed
  2. _thriftserver_ no need any extra configuration file, so just run it:
  ```vala
    /Path2Spark/sbin/start-thriftserver.sh --master spark://master:7077 --hiveconf spark.cores.max=CoreNo.
    --hiveconf spark.executor.memory=MmG
  ```
     * if you do not use _spark.cores.max=CoreNo.,spark.executor.memory=MmG_ optins, 
        __ThriftServer__ will eat resourcesses as much as it can.
     * some blogs advised to copy hive config file to _spark/conf/_ , 
        but I could run it wothout that.
  3. to run beeline (_the thrift Interface_) :
  ```prolog
    /Path2Spark/bin/beeline
    beeline> !connect jdbc:hive2://ServerName:10000
  ```
  4. _beeline Command_ are the same as [hive Commands](https://github.com/vhp1360/NoSQLandSQL/blob/master/Hadoop/Hive.md#sql-commands).

[top](#top)
# Tips
- I faced ___GC___ error when running huge data with _spark_ to write into _hadoop_, [this figured out some issues](https://stackoverflow.com/a/45570502/3214950):
  1. as always we increase `spark.shell.driver-memory`, `spark.shell.executor-memory` specially `spark.yarn.executor.memoryOverhead` 
  2. the `spark.memory.fraction` should be something like _0.4_, not _0.9_ and `spark.shuffle.memoryFraction`=0.2
  3. may need set `spark.executor.extraJavaOptions` to -XX:-UseGCOverheadLimit
  4. in __spark rpc timeout__ issue , we could deal by set `spark.network.timeout` to "600s".
- here is some type of __spark__ config in __R__:
  1. First Type:
  ```r
    config = sparkR.conf() 
    config$`sparklyr.cores.local` = 16 
    config$`sparklyr.shell.driver-memory` = "16G" 
    config$spark.memory.fraction = 0.4 
    config$spark.shuffle.memoryFraction = 0.2 
    config$spark.executor.extraJavaOptions = "-XX:-UseGCOverheadLimit" 
  ```
  2. another type(I'm not completely sure for these two, but the skeltone is correct):
  ```r
    sparkR.session() 
    allConfigs <- sparkR.conf() 
    masterValue <- unlist(sparkR.conf("spark.master")) 
    namedConfig <- sparkR.conf("spark.executor.memory", "16g") 
    namedConfig <-sparkR.conf(spark.cores.local,16) 
    namedConfig <-sparkR.conf("spark.shell.driver-memory", "16G") 
    namedConfig <-sparkR.conf("spark.memory.fraction" , "0.4") 
    namedConfig <-sparkR.conf("spark.shuffle.memoryFraction" , "0.2") 
    namedConfig <-sparkR.conf("spark.executor.extraJavaOptions" , "-XX:-UseGCOverheadLimit")
  ```
  ```r
    sparkR.conf(spark.cores.local,16) 
    sparkR.conf(spark.shell.driver-memory, "16G") 
    sparkR.conf(spark.memory.fraction , 0.4) 
    sparkR.conf(spark.shuffle.memoryFraction , 0.2) 
    sparkR.conf(spark.executor.extraJavaOptions , "-XX:-UseGCOverheadLimit") 
  ```
  3. third type:
  ```r
    sparkR.session(master = "local[16]", sparkConfig = 
        list(appName = "AppName", spark.driver.memory="24g",spark.memory.fraction = 0.4, shuffle.memoryFraction = 0.6,
              spark.driver.maxResultSize="4g", spark.executor.extraJavaOptions = "-XX:-UseGCOverheadLimit")) 
  ```
        
[top](#top)
