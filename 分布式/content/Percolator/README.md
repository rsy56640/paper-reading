# [Large-scale incremental processing using distributed transactions and notifications](https://dl.acm.org/citation.cfm?id=1924961) 论文阅读笔记

主要有2点：

- **事务提交细节（lock列，write列），相当于用 SI+锁 实现一致性**（*注意 Write Skew*）
- **2PC 细节，故障恢复**

需求：**海量数据，随机读写，跨行事务（强一致性），高吞吐量，延迟无所谓**

### 为什么 MapReduce 不能增量更新

> 参考 Ref[1]

原因是有些操作不可结合不可交换，需要计算的中间结果，不能增量更新，所以 MapReduce 要重新计算一遍整个 repo

这有个改进版 MapReduce：[Incoop: MapReduce for incremental computations](https://dl.acm.org/citation.cfm?id=2038923)

## 设计

提供两种方式：**事务** 和 **观察者机制（用于组织增量计算）**

### 事务

Percolator为每行记录都新增了一些隐藏列，这些列保证了事务的正确执行或者回滚。

- lock列：记录此行的写锁
- write列：记录数据提交时间戳

因为要求强一致性，所以用 SI+锁（**注意要防止 Write Skew**）

- prewrite 阶段：拿到所有的写锁
  - 获得开始时间戳 `start_ts`
  - 对于所有需要写入的 cell，在lock列标记时间戳为 `start_ts`（指定其中有一个为 primary，其他为 secondary，指向 primary）（**之后会阻塞读，这样做避免了 Write Skew**）
  - 拿写锁时的冲突检测
      - 如果write列的时间戳 > 自己的 `start_ts`，说明别人先提交了，自己 abort（保证强一致性）
      - 如果lock列中有时间戳，那么说明另一个写还没有提交，或者提交了没有清理锁，那么自己 abort（或者另一个事务 crash，检查 primary lock）（解决写冲突，**这里不存在什么 *first-writer-wins***）
  - 执行事务
      - 对于读操作：如果lock列上的时间戳 < 自己的 `start_ts`，那么阻塞（**阻塞读操作，这样做避免了 Write Skew**）
      - 对于写操作：已经持有锁，直接写
- commit 阶段：用提交时间戳替换锁
  - 获得提交时间戳 `commit_ts`
  - 顺序从 primary 开始
      - 更新write列为 `commit_ts`
      - 释放锁，即清空lock列（**只要 primary lock 被清空，就认为事务成功提交**）

### Failover

> 参考 Ref[2]

如果事务 crash，必须要正确维护lock列和write列信息，采用lazy模式，由之后的事务来触发。

- prewrite 阶段 crash
  -  拿锁时 crash：清理部分lock列的锁
  -  执行时 crash：清空lock列
- commit 阶段 crash
  - 如果 primary lock 还在，说明事务未被提交，清空lock列，回滚（GC？？）
  - 如果 primary lock 不在，说明事务已经成功提交，清除剩下的lock列，并且补上write列的信息

### 通知机制

通知机制组织了增量计算的任务。   
Observer 注册一个列和对应的回调函数，回调函数触发下游的 Observer 任务。   
当改变发生时，并不会立即通知 Observer，而是通过 worker 线程**异步**扫描来通知。


## Reference

- [经典论文翻译导读之《Large-scale Incremental Processing Using Distributed Transactions and Notifications》](http://www.importnew.com/2896.html)
- [Google Percolator 分布式事务实现原理解读](http://mysql.taobao.org/monthly/2018/11/02/)
- [Google Percolator事务](https://zhuanlan.zhihu.com/p/53197633)
- [Percolator论文阅读笔记](http://loopjump.com/percolator_paper_note/)
- [Percolator 论文笔记](http://int64.me/2018/Percolator%20%E8%AE%BA%E6%96%87%E7%AC%94%E8%AE%B0.html)
- [percolator-and-txn.md - PingCAP](https://github.com/pingcap/blog-cn/blob/master/percolator-and-txn.md)
- [Google Percolator 的事务模型](https://my.oschina.net/fileoptions/blog/888995)
- [Percolator简单翻译与个人理解](https://www.jianshu.com/p/05194f4b29dd)
- [分布式事务实现-Percolator](https://www.cnblogs.com/foxmailed/p/3887430.html)
- [Percolator Google的海量数据增量处理系统](https://blog.csdn.net/colorant/article/details/47271407)
- [My reading of Percolator architecture: a Google search engine component](https://blog.octo.com/en/my-reading-of-percolator-architecture-a-google-search-engine-component/)
- [Implementing Distributed Transactions the Google Way: Percolator vs. Spanner](https://medium.com/yugabyte/implementing-distributed-transactions-the-google-way-percolator-vs-spanner-6cbccfc1f2ed)
- [学习 TLA+ - Percolator Transaction](https://www.jianshu.com/p/721df5b4454b)