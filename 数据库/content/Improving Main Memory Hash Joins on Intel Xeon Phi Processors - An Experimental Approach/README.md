# [Improving Main Memory Hash Joins on Intel Xeon Phi Processors: An Experimental Approach](http://www.vldb.org/pvldb/vol8/p642-Jha.pdf) 论文阅读笔记

常用优化手段

- prefetch
- SIMD
- manual buffer：写聚合，用一个 cache line 大小的 buffer
- TLB & huge page

实验挺详细


## Reference
