# [Main-Memory Hash Joins on Multi-Core CPUs: Tuning to the Underlying Hardware](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.362.3774) 论文阅读笔记

## parallel radix partition

- 第一遍计算 histogram
- 第二遍每个线程已经知道自己在 每个partition 的 什么位置 写了（保证了顺序写 NUMA）


## Reference
