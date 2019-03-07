# Overview

Apache CarbonData 是一种在大数据平台上用于快速分析的带索引的列式存储数据格式。

## Feature

- 列式存储
- 多级索引：BTree、MinMax
- 字典编码
- 下推优化：File、Blocklet
- DDL、DML、Update、Delete
- Partition：column、hash,list,range
- DataMaps：Pre-Aggregate、Time Series、Bloom filter、Lucene、MV (Materialized Views)
- 深度集成Spark，支持Hive、Presto
- Storage：S3、HDFS、Alluxio

## File Structure

### Directory

![File Directory](../assets/images/carbondata/File-Directory.png)

### Schema

![File Schema](../assets/images/carbondata/File-Schema.png)

### Format

- Header
- Blocklet
- Footer

**Other**

- Index
- Dictionary
- Table Status

## Reference

- [Docs](http://carbondata.apache.org/documentation.html)
- [Github](https://github.com/apache/carbondata)