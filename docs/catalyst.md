# SQL Catalyst

![Catalyst](assets/images/catalyst.png)

## Tree<TreeNode>

* UnaryNode、BinaryNode、LeafNode

## Rule

## Parser

* SQL、Dataset、DataFrame -> ANTLR(词法、语法<Visitor>) -> 未绑定的逻辑计划（Relation、Function、Attribute）

## Analyzer

* Catalog、Metastore、Rule -> 数据绑定 -> 绑定的逻辑计划

## Optimizer

* RBO（Rule-Based Optimizer）
* 合并、裁剪、谓词下推

## Planner

* 策略（Strategy）
* CBO（Cost-Based Optimizer）：Shuffle、Join

## Execution

## Tungsten

* Memory Management and Binary Processing
* Cache-aware computation
* Code generation
* No virtual function dispatches
* Intermediate data in memory vs CPU registers
* Loop unrolling and SIMD

## Columnar

## Vectorization

* Parquet
* ORC
* CarbonData

## Codegen/Janino/JIT

* HashAggregate
* BroadcastHashJoin
* SortMergeJoin
* RDDScan
* DataSourceScan
* WholeStageCodegen

## Hint

* Join
* Shuffle

## Statistics

* Table(sizeInBytes、rowCount、hints)
* Column(distinctCount、min、max、nullCount、avgLen、maxLen、histogram)

## Adapter

## Data Source

## Session

## Cache

## Compression

## ShuffleService

## Reference

