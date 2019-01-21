# 调度（Schedule）

## 资源（Resource）

* 计算（CPU、GPU）
* I/O（Memory、Disk<SSD、HDD、HHD>、Network、RAID、HBA）

## 容器（Container）

* 资源隔离（Resource Isolation<CGroup>）
* 生命周期（Life Cycle）

## 资源分配（Allocation）

* 全量（Gang<MPP>）
* 增量（Incremental<DAG>）

## 调度策略（Strategy）

* FIFO 
* Capacity
* Fair
* Delay
* DRF（Domainant Reource Fair）

## 调度算法（Algorithm）

* First Fitness
* 背包问题：贪心算法
* 规划问题：整数规划
* Graph Base（Firmament）
* 强化学习

## 调度模型（Pattern）

* 资源（Yarn、Mesos、Kubernetes）
* 作业（Oozie、Airflow、Azkaban）
* 任务（Spark、TEZ、Presto）

## 调度架构（Architecture）

* 集中调度（Monolithic<Kubernetes>）
* 两级调度（Two Level<Yarn、Mesos>）
* 共享状态调度（Shared State<Omega>）
* 全分布式调度
* 混合调度

## 约束条件（Constraint）

* 资源异质性、负载异质性、亲和与反亲和、数据依赖、数据本地性、资源利用率、资源隔离、公平性、优先级、SLA、饥饿与活锁、容错

## Reference：

- [Scheduler Architectures](http://www.firmament.io/blog/scheduler-architectures.html)
- [Firmament: Fast, Centralized Cluster Scheduling at Scale](https://www.usenix.org/conference/osdi16/technical-sessions/presentation/gog)

