# Introduction

当前版本基于`Spark SQL 2.x`进行整理，参考了主流分布式`SQL`计算引擎相关的开源项目。

![Spark SQL](assets/images/sparksql.png)

* Spark Core（RDD APIs）、Data Source Connectors
* Catalyst Optimization、Tungsten Execution
* SparkSession、Dataset/DataFrame APIs、SQL
* Structured Streaming、MLlib、GraphFrame、TensorFrames

## Reference

- [Spark SQL](https://spark.apache.org/sql/): Spark SQL is Apache Spark's module for working with structured data.
- [Hive](https://cwiki.apache.org/confluence/display/Hive): The Apache Hive ™ data warehouse software facilitates reading, writing, and managing large datasets residing in distributed storage using SQL. Structure can be projected onto data already in storage. A command line tool and JDBC driver are provided to connect users to Hive.
- [Presto](https://prestodb.io/docs/current/): Distributed SQL Query Engine for Big Data.