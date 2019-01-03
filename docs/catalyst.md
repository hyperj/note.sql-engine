# SQL Catalyst

![Catalyst](assets/images/catalyst.png)

## Encoder

a container of serde expressions in Dataset

- Serialize、Deserialize
- ExpressionEncoder

## InternalRow

- UnsafeRow(Tungsten)
- JoinedRow(Join)
- BaseGenericInternalRow
  - GenericInternalRow
  - SpecificInternalRow(modify)
  - MutableUnsafeRow(update)

## TreeNode

- Expression
- QueryPlan
  - LogicalPlan
    - UnaryNode、BinaryNode、LeafNode、Other
  - SparkPlan
    - UnaryExecNode、BinaryExecNode、LeafExecNode、Other

## Rule

- Rule
- RuleExecutor
  - Once
  - FixedPoint
  - Batch

## Parser

- ANTLR(Lexer、Parser)：Adaptive LL(*)，Listener、Visitor
- SQL、Dataset、DataFrame -> AstBuilder -> Unresolved LogicalPlan（Relation、Function、Attribute）

## Analyzer

- Strategy、Rule-Based
- Catalog、Metastore、Rule -> semantically validates and transforms(resolving, removing, modifying) -> Analyzed LogicalPlan
- Batch(Substitution、Resolution、Nondeterministic、UDF、FixNullability、Cleanup)

## Optimizer

- Analyzed LogicalPlan -> RBO(Rule-Based Optimizer) -> Optimized LogicalPlan
- Rules：组合（Combine）、替换（Replace）、裁剪（Prune）、下推（Push）、消除（Eliminate）、简化（Simplify）、优化（Optimize）、改写（Rewrite）...

## Planner

- Strategy、Rule
- CBO（Cost-Based Optimizer）：Shuffle、Join

## Execution

![SparkPlan Execution](assets/images/sparkplan-execute.png)

- QueryExecution

## Aggregation

- Partial、PartialMerge、Final、Complete

### Window

```antlrv4
windowSpec
    : name=identifier  #windowRef
    | '('name=identifier')'  #windowRef
    | '('
      ( CLUSTER BY partition+=expression (',' partition+=expression)*
      | ((PARTITION | DISTRIBUTE) BY partition+=expression (',' partition+=expression)*)?
        ((ORDER | SORT) BY sortItem (',' sortItem)*)?)
      windowFrame?
      ')'              #windowDef
    ;

windowFrame
    : frameType=RANGE start=frameBound
    | frameType=ROWS start=frameBound
    | frameType=RANGE BETWEEN start=frameBound AND end=frameBound
    | frameType=ROWS BETWEEN start=frameBound AND end=frameBound
    ;

frameBound
    : UNBOUNDED boundType=(PRECEDING | FOLLOWING)
    | boundType=CURRENT ROW
    | expression boundType=(PRECEDING | FOLLOWING)
    ;
```

## Join

```antlrv4
joinRelation
    : (joinType) JOIN right=relationPrimary joinCriteria?
    | NATURAL joinType JOIN right=relationPrimary
    ;

joinType
    : INNER?
    | CROSS
    | LEFT OUTER?
    | LEFT SEMI
    | RIGHT OUTER?
    | FULL OUTER?
    | LEFT? ANTI
    ;

joinCriteria
    : ON booleanExpression
    | USING identifierList
    ;
```

## Tungsten

- Memory Management and Binary Processing
- Cache-aware computation(CPU L1/L2/L3: Cache Hit, Cache Locality)
- Code generation(Janino、WholeStageCodegen)
- No virtual function dispatches
- Intermediate data in memory vs CPU registers
- Loop unrolling and SIMD

## Columnar

in-memory columnar format

## Codegen/Janino/JIT

- HashAggregate
- BroadcastHashJoin
- SortMergeJoin
- RDDScan
- DataSourceScan
- WholeStageCodegen

## Hint

- Join
- Shuffle

## Statistics

- Table(sizeInBytes、rowCount、hints)
- Column(distinctCount、min、max、nullCount、avgLen、maxLen、histogram)

## Adapter

- Metrics

## Data Source

- Federation
- Partitions
- Transactional
- Vectorization(Pushdown)
  - Parquet
  - ORC
  - CarbonData

## Session

Application -1:n-> Session(Context) -1:n-> Job

## Catalog

- Configuration
- View
- Function<Registry、Loader>
- External Catalog<Memory、Hive>

## Cache

- persist(StorageLevel.MEMORY_AND_DISK)

## Compression

- Cache tables in-memory columnar format
- Compression batchSize default 10000

## ShuffleService

- Standalone Mode
- Executor process

## Reference

- [Spark SQL: Relational Data Processing in Spark](http://people.csail.mit.edu/matei/papers/2015/sigmod_spark_sql.pdf)
- [Deep Dive into Spark SQL’s Catalyst Optimizer](https://databricks.com/blog/2015/04/13/deep-dive-into-spark-sqls-catalyst-optimizer.html)
- [Cost Based Optimizer in Apache Spark 2.2](https://databricks.com/blog/2017/08/31/cost-based-optimizer-in-apache-spark-2-2.html)
- [Datasource V2 Series](http://blog.madhukaraphatak.com/categories/datasource-v2-series/)
- [LL parser](https://en.wikipedia.org/wiki/LL_parser)
