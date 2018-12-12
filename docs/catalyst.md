# SQL Catalyst

![Catalyst](assets/images/catalyst.png)

## InternalRow

* UnsafeRow
* JoinedRow
* BaseGenericInternalRow
  * GenericInternalRow
  * SpecificInternalRow
  * MutableUnsafeRow

## TreeNode

## QueryPlan

- LogicalPlan

  UnaryNode、BinaryNode、LeafNode、Other

- SparkPlan

  UnaryExecNode、BinaryExecNode、LeafExecNode、Other

## Rule

* Rule
* RuleExecutor

## Parser

* SQL、Dataset、DataFrame -> ANTLR(词法、语法<Visitor>) -> 未绑定的逻辑计划（Relation、Function、Attribute）

## Analyzer

* Catalog、Metastore、Rule -> 数据绑定 -> 绑定的逻辑计划
* Batch(Substitution、Resolution、Nondeterministic、UDF、FixNullability、Cleanup)

## Optimizer

* RBO（Rule-Based Optimizer）
* 组合、裁剪、下推、消除、简化、优化

## Planner

* 策略（Strategy）
* CBO（Cost-Based Optimizer）：Shuffle、Join

## Execution

### Aggregation

### Join

## Tungsten

* Memory Management and Binary Processing
* Cache-aware computation(CPU L1/L2/L3: Cache Hit, Cache Locality)
* Code generation(Janino、WholeStageCodegen)
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

* Federation

## Session

## Catalog

* Configuration
* View
* Function<Registry、Loader>
* External Catalog<Memory、Hive>

## Cache

## Compression

## ShuffleService

## Reference

* [Spark SQL: Relational Data Processing in Spark](http://people.csail.mit.edu/matei/papers/2015/sigmod_spark_sql.pdf)
* [Deep Dive into Spark SQL’s Catalyst Optimizer](https://databricks.com/blog/2015/04/13/deep-dive-into-spark-sqls-catalyst-optimizer.html)
* [Cost Based Optimizer in Apache Spark 2.2](https://databricks.com/blog/2017/08/31/cost-based-optimizer-in-apache-spark-2-2.html)
