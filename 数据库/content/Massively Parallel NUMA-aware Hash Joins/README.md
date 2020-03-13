# [Massively Parallel NUMA-aware Hash Joins](https://link.springer.com/chapter/10.1007/978-3-319-13960-9_1) 论文阅读笔记

- no partition
- shared partition
- indepdent partition

hash build 只有 insert

并发问题（其实我觉得只要决定了控制流和数据流，并发的方案进本就确定了，剩下的无非是写代码的问题。很多居然是把辣鸡代码改成正常就叫做优化了。。。）

实验分析

- 并发
- NUMA 内存分配

## Reference
