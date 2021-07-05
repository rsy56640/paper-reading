# Record Computer Architecture Papers Reading

- [CPU](#cpu)
- [Cache](#cache)
- [Memory](#memory)


&nbsp;  
<a id="cpu"></a>
## CPU

- [Processor Microarchitecture an Implementation Perspective 读书笔记](https://github.com/rsy56640/Computer_Architecture_learning/tree/master/Processor%20Microarchitecture%20An%20Implementation%20Perspective%20%E7%AC%94%E8%AE%B0)


&nbsp;  
<a id="cache"></a>
## Cache

- [A Survey of Side-Channel Attacks on Caches and Countermeasures](https://link.springer.com/article/10.1007/s41635-017-0025-y) 通过测量 cache timing 来获取关键数据

### Replacement Policy

- [High performance cache replacement using re-reference interval prediction (RRIP)](https://dl.acm.org/doi/abs/10.1145/1815961.1815971) RRIP 探讨 mixed cache access pattern 以及 re-reference interval 更新策略


&nbsp;  
<a id="memory"></a>
## Memory

- [Flipping bits in memory without accessing them: an experimental study of DRAM disturbance errors 论文阅读笔记](https://github.com/rsy56640/paper-reading/tree/master/%E4%BD%93%E7%B3%BB%E7%BB%93%E6%9E%84/content/Flipping%20Bits%20in%20Memory%20Without%20Accessing%20Them%20-%20An%20Experimental%20Study%20of%20DRAM%20Disturbance%20Errors)

### TLB & Page table

- [Design tradeoffs for software-managed TLBs](https://dl.acm.org/doi/10.1145/165123.165127)
- [Reverse Engineering Hardware Page Table Caches Using Side-Channel Attacks on the MMU](https://download.vusec.net/papers/revanc_ir-cs-77.pdf) 对 Page Table Cache 做 EVICT+TIME
- [Translation caching: skip, don't walk (the page table) 笔记](https://github.com/rsy56640/paper-reading/tree/master/%E4%BD%93%E7%B3%BB%E7%BB%93%E6%9E%84/content/Translation%20Caching%20-%20Skip%2C%20Don%E2%80%99t%20Walk%20(the%20Page%20Table)) MMU cache 加速 page table walk

