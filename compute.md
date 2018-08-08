# 计算（Compute）

### Pattern

* MR、MRM（Map、Reduce、Merge）
* 可枚举性（Ad hoc、OLAP）、可加性（批量、增量&lt;State&gt;）

### 约束条件（Constraint）

### RDD

#### Characteristics

* Partitions
* PreferredLocations
* Dependencies
* Iterator
* Partitioner

#### Operations

* Creation
* Transformation
* Storage
* Action

#### Dependencies

* Narrow Dependencies
* Shuffle/Wide Dependencies

### Stage

* ResultStage
* ShuffleMapStage

### DAG

### Shuffle



### Tungsten

* Memory Management and Binary Processing
* Cache-aware computation
* Code generation
* No virtual function dispatches
* Intermediate data in memory vs CPU registers
* Loop unrolling and SIMD

## Reference

