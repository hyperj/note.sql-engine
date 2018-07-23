# SQL（Catalyst Optimizer）

![Catalyst](.gitbook/assets/catalyst.png)

#### Tree&lt;TreeNode&gt; 

> UnaryNode、BinaryNode、LeafNode

#### Rule

#### Parser

> SQL、Dataset、DataFrame -&gt; 词法、语法 解析 -&gt; 未绑定的逻辑计划（Relation、Function、Attribute）

#### Analyzer

> Catalog、Metastore -&gt; 数据绑定 -&gt; 绑定的逻辑计划

#### Optimizer

> RBO（Rule-Based Optimizer）
>
> 合并、裁剪、谓词下推

#### Planner

> 策略
>
> CBO（Cost-Based Optimizer）：Shuffle、Join

#### Execution

>

#### Codegen

#### Vectorization

#### Columnar

#### Session

#### Cache

#### Compression

#### ShuffleService



