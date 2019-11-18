# [Column-Stores vs. Row-Stores - How Different Are They Really](https://dl.acm.org/citation.cfm?id=1376712) 阅读笔记

> 这篇文章有点老，在2019年差不多没啥看的

## NSM Execution

- vertical partitioned
- index
- materialized view

### Vertical Partitioning

每个 attribute 作为一列，如果不定长就附加一列 position。通常还是给定长 block，这样一个元素在列中的位置可以直接计算

### Index-only plan

每个列都有非聚簇 index，有时对 composite key 建立索引，避免访问多个 index

### Materialized View

对 query 中要访问的列提取出来，建立 view，减少其他不必要的访问


## DSM Execution

### Compression

### Late Materialization

为了得到 row，需要拼接，称作 materialization 或 tuple construction

### Block Iteration

### Invisible Join

## 总结

在 row store 上模拟 column store 影响性能，因为 tuple reconstruction


## Reference

- [CMU Advanced Database Systems - 09 Storage Models & Data Layout (Spring 2019)](https://www.youtube.com/watch?v=BuKmw3CFHYY&list=PLSE8ODhjZXja7K1hjZ01UTVDnGQdx5v5U&index=9)