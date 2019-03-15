# Columnar and Vectorization

## 列存

行存，以行为形式组织存储，一行是一个tuple存在一起；列存，以列为形式组织存储，每列对应一个或一批文件

- 压缩(Compression)
- 块遍历(Block Iteration)
- 向量化(Vectorization)
- 延迟物化(Late Materialization)

## 向量化

向量化计算是一种特殊的并行计算的方式，相比于一般程序在同一时间只执行一个操作的方式，它可以在同一时间执行多次操作，通常是对不同的数据执行同样的一个或一批指令，或者说把指令应用于一个数组/向量。

向量化的处理方式是现代计算机的一个特点，无论硬件还是软件上，都提供了支持。

- SIMD(Single Instruction Multiple Data, 单指令多数据流) 

SIMD 采用和并发无关的数据级并行。SIMD 指令允许在同一时钟周期内，对不同的列数据执行相同的指令, 实际上执行吞吐量（throughput of execution）可以提高 4 倍或更多。列式数据可以遵循 SIMD 处理，这样可以存储列值到内存中的有序排列且字节对齐的密集数组中，这些数据会载入到固定宽度的 SIMD 寄存器中。

- JIT(Just In Time Compiler)

LLVM 是一组模块化、可复用的编译框架和工具链的集合，编译框架用来实现动态生成代码 Codegen

Spark 使用了 Janino 作为代码生成的默认 Compiler

## Reference

- [列式数据库和向量化](https://infoq.cn/article/columnar-databases-and-vectorization)
- [PgSQL · 引擎介绍 · 向量化执行引擎简介](http://mysql.taobao.org/monthly/2017/01/06/)
- [《Column-Stores vs. Row-Stores》读后感](https://zhuanlan.zhihu.com/p/54433448)
