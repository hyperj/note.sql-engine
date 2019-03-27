# SQL Engine

## 场景

计算可枚举，可优化查询或存储，提升效率

- Ad hoc
- MPP
- OLAP
  - MOPLAP
  - ROLAP
  - HOLAP
- OLTP

## 计划

- Parser
- Analyzer
- Optimizer
- Planner
- Execution

## 调度

- FIFO 
- Fair
- Delay
- DRF

## 计算

- DAG
- MRM
- Codegen
- Stage
- Task

## 存储

- NSM：Row-oriented，OLTP
- DSM：Column-oriented，OLAP
- HTAP：
  - PAX（Partition Attributes Across）
    
## 索引

- 稀疏索引
- 多级索引
- B+Tree
- LSM-Tree
- 位图索引（BitMap）
- 倒排索引（Inverted）
- BloomFilter
- SkipList

## 其他

- 数据更新
- 实时数据
- 复杂查询
- 自定义函数
- 精确去重
- 预计算
- 物化视图
- 数据量级
- 内存依赖
- 并发度
- 事务
- 社区活跃度
- 可扩展性
- 可维护性

## Reference
