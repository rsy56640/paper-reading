# Diva：Making MVCC Systems HTAP-Friendly 论文笔记

<img src="assets/Fig1.png" width="600"/>

通常存在两个维度的耦合：

- MVCC 和 RECOVERY：是不是用 UNDO 做 MVCC
- 版本查找和回收

两个维度的解耦目标

- 已提交和未提交的放在 page 上，其他版本单独存储
- 版本搜索与版本回收分开，各自做优化

## 3 DESIGN OVERVIEW OF DIVA

<img src="assets/Fig2.png" width="600"/>

- 版本存储额外分出去，并且构建临时索引，提供分离的异步清理的能力

## 4 PROVISIONAL VERSION INDEXING

<img src="assets/Fig3.png" width="600"/>

引入简介层，存版本地址，减少遍历版本链引发的IO（最多2次）

<img src="assets/Fig4.png" width="600"/>

- macro compaction：ROW + deferred reclaimation
- micro compaction：前台事务压缩

## 5 VERSION GARBAGE COLLECTION

- 判断版本不可见
- 执行回收动作

<img src="assets/Fig5.png" width="600"/>
<img src="assets/Fig6.png" width="600"/>

按照固定间隔分割 epoch 来构成叶子层，并且对该 epoch 的活跃事务计数。当某个区间计数为0就可以回收生命周期落在该区间的版本。由于一个版本生命周期可能跨越多个区间，所以需要一个结构能够表示连续区间的计数，并且每个区间能够记录其相关的版本。

interval tree

- 不需要旋转，并发性能差
- lockfree 操作

<img src="assets/Fig7.png" width="960"/>

<img src="assets/Fig8.png" width="600"/>

- insert new epoch
  - 从最右边开始往上找，直到一个节点 node，其左子树范围 > 右子树范围，没有就在最上面新建一个
  - 该 node 的右子树新建一个节点，左边放原来的右子树，右边放 new epoch
  - 如果没有删除，就会形成完全二叉树
- delete epoch
  - 向上收缩，如果一个节点只有一个子节点，那么该节点被干掉（当然会有一个 grace period 保证并发访问安全）
  - 注意该节点允许继承之前的区间，因为可能还要有版本向该区间加入（这里为什么不用自己作为区间，而是要使用原来父节点的区间并且接受对应的版本？如果使用自己作为区间，那么有版本过来没有命中，可以直接删除）

<img src="assets/Fig9.png" width="600"/>

最坏的插入情况，每次插入都新增 root

<img src="assets/Thm1.png" width="600"/>

最大高度只依赖于最小活跃事务，也就是 epoch 区间宽度

## 6 DESIGN PRINCIPLES IN ACTION

- 在 MySQL8.0 上实现了 provisional index 机制，但是由于 undo 是 增量 log，需要遍历回放，不能直接寻址到对应 record
- 触发 macro compaction 的指标：p-leaf index 和 interval tree 的空间差异。因为 p-leaf index 只会增长，中间出现空洞，而 interval tree 可以收缩避免空洞
- 如何实现 p-leaf index 整合到 DB：pk record header 找地方放 locator 指向 p-leaf index（需要考虑 DB mark-delete）

<img src="assets/Fig10.png" width="600"/>

- GC 优化：在放置版本时从 root 向下遍历，如果
  - 与 2 个孩子节点相交，那么停止
  - 与 1 个孩子节点相交，继续向下
  - 与 0 个孩子节点相交，可以直接删除
  - 没有孩子节点，加入对应版本集合

## 7 EXPERIMENTAL EVALUATION

<img src="assets/Fig11.png" width="600"/>

- MySQL 长事务版本搜索时间变长，引发页面竞争影响 TP
- Postgres 短事务搜索时间长，因为 old2new
- 在 HTAP 中，即使有少量IO，对性能影响也很大
- 基于间隔的版本回收节省了 90% 的存储空间

<img src="assets/Fig12.png" width="600"/>

- OLAP 导致 IO 增多，并且引起缓冲区竞争导致 TP 时延上升

<img src="assets/Fig13.png" width="600"/>

- 版本较少，所以影响不大

<img src="assets/Fig14.png" width="600"/>

<img src="assets/Fig15.png" width="600"/>

<img src="assets/Fig16.png" width="600"/>

- DIVA 可以显著减少缓冲区竞争

<img src="assets/Fig17.png" width="600"/>

- 在达到缓冲区容量前，主要是锁开销
- 缓冲区竞争导致大量锁和IO开销

<img src="assets/Fig18.png" width="600"/>
<img src="assets/Fig19.png" width="600"/>
<img src="assets/Fig20.png" width="600"/>

- 与 Fig11 相比，在 skewed workload 下，PostgreSQL TP 需要遍历更长的版本链

## REFERENCE

- [有slide](https://www.zhihu.com/question/524369148/answer/2673645895)