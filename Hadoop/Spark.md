<div dir=rtl>بنام خدا</div>

- [Tips](#tips)



# Tips
- I faced ___GC___ error when running huge data with _spark_ to write into _hadoop_, [this figured out some issues](https://stackoverflow.com/a/45570502/3214950):
  1. as always we increase `spark.shell.driver-memory`, `spark.shell.executor-memory` specially `spark.yarn.executor.memoryOverhead` 
  2. the `spark.memory.fraction` should be something like _0.4_, not _0.9_ and `spark.shuffle.memoryFraction`=0.2
  3. may need set `spark.executor.extraJavaOptions` to -XX:-UseGCOverheadLimit
  4. in __spark rpc timeout__ issue , we could deal by set `spark.network.timeout` to "600s".
