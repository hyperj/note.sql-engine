# 计算（Compute）

## Pattern

* MR、MRM（Map、Reduce、Merge）
* 可枚举性（Ad hoc、OLAP）、可加性（批量、增量<State>）

## 约束条件（Constraint）

## RDD

### Characteristics

* Partitions
* PreferredLocations
* Dependencies
* Iterator
* Partitioner

### Operations

* Creation
* Transformation
* Storage
* Action

### Dependencies

* Narrow Dependencies
* Shuffle/Wide Dependencies

## Stage

* ResultStage
* ShuffleMapStage

## DAG

* Lineage

## Shuffle

* Read/Write
* Server/Client
* Pull/Push

## Tungsten

* Memory Management and Binary Processing
* Cache-aware computation
* Code generation
* No virtual function dispatches
* Intermediate data in memory vs CPU registers
* Loop unrolling and SIMD

## Reference

- [Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing](http://people.csail.mit.edu/matei/papers/2012/nsdi_spark.pdf)