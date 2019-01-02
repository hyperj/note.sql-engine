# 存储（Storage）

## 存储级别（Storage Level）

* Disk
* Memory
* OffHeap
* Serialization
* Replication

## 操作（Operation）

LRU(Least Recently Used)

* Cache(persist(StorageLevel.MEMORY_AND_DISK))
* Persist(persist/unPersist/destroy)
* Checkpoint

## 存储（Store）

* Disk
* Memory(OnHeap/OffHeap)

## 统一内存管理（Unified Memory Management）

* Execution
* Storage

## 会话（Session）

* Metastore
* Local Session
* Global Session

## 洗牌（Shuffle）

* Read/Write
* Server/Client
* Pull/Push

## 存储格式（Storage Format）

* ORC
* Parquet
* CarbonData

## Reference

- [Apache Spark 内存管理详解](https://www.ibm.com/developerworks/cn/analytics/library/ba-cn-apache-spark-memory-management/)
- [Spark Storage ① - Spark Storage 模块整体架构](https://www.jianshu.com/p/730eed6a98d2)
- [Spark Storage ② - BlockManager 的创建与注册](https://www.jianshu.com/p/356db9726d04)
- [Spark Storage ③ - Master 与 Slave 之间的消息传递与时机](https://www.jianshu.com/p/7a7ff2c19635)
- [Spark Storage ④ - 存储执行类介绍（DiskBlockManager、DiskStore、MemoryStore）](https://www.jianshu.com/p/19e36d0781b5)
- [Spark 内存管理的前世今生（上）](https://www.jianshu.com/p/999ef21dffe8)
- [Spark 内存管理的前世今生（下）](https://www.jianshu.com/p/211505ae3fb3)