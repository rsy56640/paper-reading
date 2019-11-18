# [Hybrid Garbage Collection for Multi-Version Concurrency Control in SAP HANA](https://dl.acm.org/citation.cfm?id=2903734) 论文阅读笔记

GC 的基本方法是把所有 commit-ts < 最小的 txn 的 version 回收（除了最后的）。但是 OLAP 会有 long-lived read txn，ts 比较小，在这个 read duration 中的 version 都不会被回收（但部分其实可以）

## SAP HANA

- version storage
  - table space 存 original (oldest)，在 GC 时可能被更新
  - version space 是 newest to oldest

<img src="./assets/sap_hana_version_storage.png" width="800"/>


## Garbage Collector

### Timestamp

与 global minimum txn-ts 比较

### Interval Garbage Collector

**如果没有 txn-ts 落在2个连续 version 之间，那么较早的 version 可以被清除。**

### Single / Group Garbage Collector


## GC in SAP HANA

- group version + timestamp
- single version + interval
- table garbage collectors

### Group Garbage Collector

<img src="./assets/global_snapshot_timestamp_tracker.png" width="400"/>

维护一个全局 txn-ts list，node 使用 ref count

<img src="./assets/global_group_gc.png" width="400"/>

GC 的单位是 txn group

### Interval Garbage Collector

从 GroupCommitContext 里面 > min-ts 的开始，遍历 version chain，检查 interval

### Table GC

<img src="./assets/table_gc.png" width="400"/>

如果可以预先知道哪些 table 会被访问，那么就可以做出优化。那些最近不会被访问的 table 就可以做 GC

### HybridGC

<img src="./assets/hybrid_gc.png" width="800"/>

- 先粗粒度 group version GC，然后 table GC 或者 interval GC
- table GC 检查 GroupCommitContext 的子集，回收 < global-min-ts
- interval GC 检查所有 version chain


## Reference

- [CMU Advanced Database Systems - 05 MVCC Garbage Collection (Spring 2019)](https://www.youtube.com/watch?v=AD1HW9mLlrg&list=PLSE8ODhjZXja7K1hjZ01UTVDnGQdx5v5U&index=6&t=0s)