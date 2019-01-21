# Catalyst

![Catalyst](assets/images/catalyst.png)

## Encoder

a container of serde expressions in Dataset

- Serialize、Deserialize
- ExpressionEncoder(only)

_RowEncoder(mapping & convert external rows)_

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
    - resolved、canonicalized
    - UnaryNode、BinaryNode、LeafNode、Other
  - SparkPlan
    - UnaryExecNode、BinaryExecNode、LeafExecNode、Other

## Rule

- Rule
- RuleExecutor
  - Seq[Batch]
  - Strategy
    - Once
    - FixedPoint

## Parser

- ANTLR(Lexer、Parser)：Adaptive LL(*)，Listener、Visitor
- SQL、Dataset、DataFrame -> AstBuilder -> Unresolved LogicalPlan（Relation、Function、Attribute）

## Analyzer

![LogicalPlan Analyzer](assets/images/logicalplan-analyzer.png)

- Strategy、Rule-Based
- Catalog、Metastore、Rule -> semantically validates and transforms(resolving, removing, modifying) -> Analyzed LogicalPlan

| Batch | Strategy | Rules |
| :--- | :--- | :--- |
| Hints | FixedPoint | ResolveBroadcastHints、ResolveCoalesceHints、RemoveAllHints |
| Simple Sanity Check | Once | LookupFunctions |
| Substitution | FixedPoint | CTESubstitution、WindowsSubstitution、EliminateUnions、SubstituteUnresolvedOrdinals |
| Resolution | FixedPoint | ResolveTableValuedFunctions、ResolveRelations、ResolveReferences、ResolveCreateNamedStruct、ResolveDeserializer、ResolveNewInstance、ResolveUpCast、ResolveGroupingAnalytics、ResolvePivot、ResolveOrdinalInOrderByAndGroupBy、ResolveMissingReferences、ExtractGenerator、ResolveGenerate、ResolveFunctions、ResolveAliases、ResolveSubquery、ResolveWindowOrder、ResolveWindowFrame、ResolveNaturalAndUsingJoin、ExtractWindowExpressions、GlobalAggregates、ResolveAggregateFunctions、TimeWindowing、ResolveInlineTables、TypeCoercion.typeCoercionRules、extendedResolutionRules |
| Post-Hoc Resolution | Once | postHocResolutionRules |
| View | Once | AliasViewChild |
| Nondeterministic | Once | PullOutNondeterministic |
| UDF | Once | HandleNullInputsForUDF |
| FixNullability | Once | FixNullability |
| ResolveTimeZone | Once | ResolveTimeZone |
| Cleanup | FixedPoint | CleanupAliases |

## Optimizer

- Analyzed LogicalPlan -> RBO(Rule-Based Optimizer) -> Optimized LogicalPlan

| Batch | Strategy | Rules |
| :--- | :--- | :--- |
| Eliminate Distinct | FixedPoint | EliminateDistinct |
| Finish Analysis | Once | EliminateSubqueryAliases、EliminateView、ReplaceExpressions、ComputeCurrentTime、GetCurrentDatabase、RewriteDistinctAggregates、ReplaceDeduplicateWithAggregate |
| Union | Once | CombineUnions |
| LocalRelation early | FixedPoint | ConvertToLocalRelation、PropagateEmptyRelation |
| Pullup Correlated Expressions | Once | PullupCorrelatedPredicates |
| Subquery | Once | OptimizeSubqueries |
| Replace Operators | FixedPoint | RewriteExceptAll、RewriteIntersectAll、ReplaceIntersectWithSemiJoin、ReplaceExceptWithFilter、ReplaceExceptWithAntiJoin、ReplaceDistinctWithAggregate |
| Aggregate | FixedPoint | RemoveLiteralFromGroupExpressions、RemoveRepetitionFromGroupExpressions |
| Join Reorder | Once | CostBasedJoinReorder |
| Remove Redundant Sorts | Once | RemoveRedundantSorts |
| Decimal Optimizations | FixedPoint | DecimalAggregates |
| Object Expressions Optimization | FixedPoint | EliminateMapObjects、CombineTypedFilters |
| LocalRelation | FixedPoint | ConvertToLocalRelation、PropagateEmptyRelation |
| Extract PythonUDF From JoinCondition | Once | PullOutPythonUDFInJoinCondition |
| Check Cartesian Products | Once | CheckCartesianProducts |
| RewriteSubquery | Once | RewritePredicateSubquery、ColumnPruning、CollapseProject、RemoveRedundantProject |
| UpdateAttributeReferences | Once | UpdateNullabilityInAttributeReferences |

- extendedOperatorOptimizationRules

PushProjectionThroughUnion、ReorderJoin、EliminateOuterJoin、PushPredicateThroughJoin、PushDownPredicate、LimitPushDown、ColumnPruning、CollapseRepartition、CollapseProject、CollapseWindow、CombineFilters、CombineLimits、CombineUnions、NullPropagation、ConstantPropagation、FoldablePropagation、OptimizeIn、ConstantFolding、ReorderAssociativeOperator、LikeSimplification、BooleanSimplification、SimplifyConditionals、RemoveDispensableExpressions、SimplifyBinaryComparison、PruneFilters、EliminateSorts、SimplifyCasts、SimplifyCaseConversionExpressions、RewriteCorrelatedScalarSubquery、EliminateSerialization、RemoveRedundantAliases、RemoveRedundantProject、SimplifyExtractValueOps、CombineConcats

- Non-Excludable

PushProjectionThroughUnion、EliminateDistinct、EliminateSubqueryAliases、EliminateView、ReplaceExpressions、ComputeCurrentTime、GetCurrentDatabase、RewriteDistinctAggregates、ReplaceDeduplicateWithAggregate、ReplaceIntersectWithSemiJoin、ReplaceExceptWithFilter、ReplaceExceptWithAntiJoin、RewriteExceptAll、RewriteIntersectAll、ReplaceDistinctWithAggregate、PullupCorrelatedPredicates、RewriteCorrelatedScalarSubquery、RewritePredicateSubquery、PullOutPythonUDFInJoinCondition

## Planner & Execution

![SparkPlan Execution](assets/images/sparkplan-execute.png)

- CBO（Cost-Based Optimizer）：Shuffle、Join
- SparkPlan、SparkPlaner、QueryExecution
- Distribution、Partitioning、SortOrder
- SparkPlanInfo(metadata、metrics)
- SparkStrategy(Aggregation、BasicOperators、FlatMapGroupsWithStateStrategy、InMemoryScans、JoinSelection、SpecialLimits、StatefulAggregationStrategy、StreamingDeduplicationStrategy、StreamingRelationStrategy)
- Rule(CollapseCodegenStages、PlanSubqueries、ReuseSubquery、ReuseExchange、EnsureRequirements)

## Aggregation

- Aggregation Buffer(Schema、Attributes)
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

- Join、Shuffle
- BROADCASTJOIN、MAPJOIN、STREAMTABLE、INDEX、COALESCE、REPARTITION

## Statistics

- Table(sizeInBytes、rowCount、hints)
- Column(distinctCount、min、max、nullCount、avgLen、maxLen、histogram)

## Adapter

- Metadata
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

- Application -1:n-> Session(Context) -1:n-> Job
- Share & Cache Data

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
- Executor Process

## Reference

- [Spark SQL: Relational Data Processing in Spark](http://people.csail.mit.edu/matei/papers/2015/sigmod_spark_sql.pdf)
- [Deep Dive into Spark SQL’s Catalyst Optimizer](https://databricks.com/blog/2015/04/13/deep-dive-into-spark-sqls-catalyst-optimizer.html)
- [Cost Based Optimizer in Apache Spark 2.2](https://databricks.com/blog/2017/08/31/cost-based-optimizer-in-apache-spark-2-2.html)
- [Datasource V2 Series](http://blog.madhukaraphatak.com/categories/datasource-v2-series/)
- [LL parser](https://en.wikipedia.org/wiki/LL_parser)
