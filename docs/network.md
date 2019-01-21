# 网络（Network）

## 通信机制

* RPC（Remote Procedure Call）：Protocol Buffer、Thrift、Avro（IDL、Serialization）
* Message：Queue、Pub-Sub（Pull、Push）
* Multi Broadcast：Gossip（Best Effort、Anti-Entropy<Push、Pull、Push-Pull>、Rumor Mongering）

## 角色（Role）

Master, Worker, Client, Driver, Executor

## RPC

_基于Netty_

* Context（上下文：Local、Remote）
* Env（运行环境）
* Endpoint（终端）

## 主要作用

* 消息互通：Event、Status
* 文件传输：Fetch、Upload
* Block：Store、Replication
* Shuffle：Writer、Reader

## Reference

- [体系化认识RPC](http://www.infoq.com/cn/articles/get-to-know-rpc)
- [深入解析Spark中的RPC](https://zhuanlan.zhihu.com/p/28893155)