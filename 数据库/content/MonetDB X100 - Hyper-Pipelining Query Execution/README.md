# [MonetDB/X100: Hyper-Pipelining Query Execution](http://cidrdb.org/cidr2005/papers/P19.pdf) 论文阅读笔记

所谓的 control dependency -> data dependency 现在是否有作用还值得考量。现代处理器可以对两个分支都执行，最终 retire non-bogus uops；如果是数据依赖，指令会在 reservation station 等待。

cache friendly 非常重要

- index
- OLAP 的数据流
  - branch pattern
  - fit in cacheline
  - 按块计算，掩盖 cache miss
- 有效 instruction
- NSM & DSM

## Reference
