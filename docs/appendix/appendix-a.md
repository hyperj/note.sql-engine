# 附录 A（Appendix A）

Application -1:n-> Session(Context) -1:n-> Job -1:n-> Stage

Task -1:n-> Partition -1:n-> Block

## Configuration

### Application Properties

| 名称 | 版本 | 默认值 | 推荐值 | 含义 |
| :--- | :--- | :--- | :--- | :--- |
| spark.driver.memory | - | 1g | 2g, 4g | Driver 内存 |
| spark.driver.cores | - | 1 | 2, 4 | Driver 核数 |
| spark.executor.memory | - | 1g | 4g, 16g | Executor 内存 |
| spark.executor.cores | - | 1 | 2, 8 | Executor 核数 |

### Runtime Environment

### Shuffle Behavior

### Compression and Serialization

### Memory Management

### Execution Behavior

### Networking

### Scheduling

### Dynamic Allocation

### Spark SQL

| 名称 | 版本 | 默认值 | 推荐值 | 含义 |
| :--- | :--- | :--- | :--- | :--- |
| spark.sql.shuffle.partitions | - | 200 | 20, 400 | Shuffle分区数量（Join、Aggr） |
| spark.sql.autoBroadcastJoinThreshold | - | 10L * 1024 * 1024 | (32, 64) * 1024 * 1024 | 自动优化为BroadcastJoin阈值 |
| spark.sql.adaptive.enabled | - | false | true | 自适应查询执行（Broadcast、Partition、Skew） |
| spark.sql.adaptive.shuffle.targetPostShuffleInputSize | - | 64 * 1024 * 1024 | (32, 128) * 1024 * 1024 | Shuffle读取文件大小 |
| spark.sql.adaptive.minNumPostShufflePartitions | - | -1 | 10, 200 | Shuffle最小分区数量 |

## Yarn

## Hive

| 名称 | 版本 | 默认值 | 推荐值 | 含义 |
| :--- | :--- | :--- | :--- | :--- |
| hive.exec.dynamic.partition | - | false | true | 允许动态分区 |
| hive.exec.dynamic.partition.mode | - | strict | nonstrict | 动态分区模式 |
| hive.exec.max.dynamic.partitions | - | 1000 | 100-1000 | 允许创建最大分区数 |

## MapReduce

## HDFS

## JVM

## Reference

- [Spark Configuration](https://spark.apache.org/docs/latest/configuration.html)
- [SQLConf.scala](https://github.com/apache/spark/blob/master/sql/catalyst/src/main/scala/org/apache/spark/sql/internal/SQLConf.scala)


