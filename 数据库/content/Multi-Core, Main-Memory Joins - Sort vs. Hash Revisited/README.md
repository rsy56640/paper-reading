# [Multi-Core, Main-Memory Joins - Sort vs. Hash Revisited](http://www.vldb.org/pvldb/vol7/p85-balkesen.pdf) 论文阅读笔记

## sort-merge join

- bitonic sorting
- memory bandwidth

## hash join

- partition，为了 TLB-friendly 对每一个 partition 做一个固定大小的 buffer，满了才移动到对应的 partition

### 最后讲了各种方案的实验，还有对 NUMA 的考虑，回头再看

## Reference
