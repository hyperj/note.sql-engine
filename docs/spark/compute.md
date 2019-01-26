# 计算（Compute）

## RDD

### Characteristics

- 分布（Partitions）
- 本地化（PreferredLocations）
- 依赖（Dependencies）
- 迭代（Iterator）
- 分区（Partitioner）

### Operations

- Creation
- Transformation
- Storage
- Action

### Dependencies

- Narrow Dependencies
- Shuffle/Wide Dependencies

## Stage

- ResultStage
- ShuffleMapStage

## DAG

- Lineage
- Fault Tolerance
- Data Dependency

## Shuffle

- Read/Write
- Server/Client
- Pull/Push

## Tungsten

- Memory Management and Binary Processing
- Cache-aware computation
- Code generation
- No virtual function dispatches
- Intermediate data in memory vs CPU registers
- Loop unrolling and SIMD

## Reference

- [Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing](http://people.csail.mit.edu/matei/papers/2012/nsdi_spark.pdf)