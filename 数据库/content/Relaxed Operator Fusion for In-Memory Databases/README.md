# [Relaxed Operator Fusion for In-Memory Databases - Making Compilation, Vectorization, and Prefetching Work Together At Last](http://www.vldb.org/pvldb/vol11/p1-menon.pdf) 论文阅读笔记

向量化处理可以部分掩盖缓存缺失，为题就在于不同算子之间如何传递 vector

- 数据组织形式
  - table 结点提供
      - tuple 迭代器（大概率）
      - tuple 数组
      - 列存
- join probe 侧的 source 结点


## Reference
