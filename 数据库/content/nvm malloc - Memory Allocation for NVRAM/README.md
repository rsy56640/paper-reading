# [nvm_malloc: Memory Allocation for NVRAM](http://www.adms-conf.org/2015/adms15_schwalb.pdf) 论文阅读笔记

> 没太看懂，元数据到底分布在哪里。。。   

<p/><img src="assets/Table1.png" width="480"/>
<p/><img src="assets/Table2.png" width="480"/>

## NVM Malloc

<p/><img src="assets/Fig1.png" width="600"/>

<p/><img src="assets/Table3.png" width="480"/>

- 重启时通过 id 来找到 root，然后找到整个数据结构

<p/><img src="assets/List1.png" width="480"/>

<p/><img src="assets/Table4.png" width="480"/>
<p/><img src="assets/Table5.png" width="480"/>

### Arena

<p/><img src="assets/Fig2.png" width="720"/>

<p/><img src="assets/arena_internal.png" width="720"/>

- reserve
- activate
  - bit index

### Allocation by ID

<p/><img src="assets/Fig3.png" width="600"/>

- root obj 用 id 来 alloc，方便之后寻址
- 用 volatile hashmap 加速查找

### Recovery

## Reference

- [ppt](http://www.adms-conf.org/2015/nvm_malloc.pdf)
- [nvm_malloc: Memory Allocation for NVRAM [Paper Review] - GHC 6023](https://wangziqi2013.github.io/paper/2019/11/09/nvm-malloc.html)