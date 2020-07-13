# Record Database Papers Reading

- [Architecture](#arch)
- [NSM & DSM](#storage-model)
- [Query](#query)
- [Index](#index)
- [Concurrency Control](#cc)
- [Buffer Pool](#buffer)
- [Log & Recovery](#recovery)
- [GC](#gc)


&nbsp;   
<a id="arch"></a>
## Architecture

- [System R - Relational Approach to Database Management](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/System%20R%20-%20Relational%20Approach%20to%20Database%20Management) todo
- [Architecture of a Database System](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Architecture%20of%20a%20Database%20System) todo
- [Socrates - The New SQL Server in the Cloud](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Socrates%20-%20The%20New%20SQL%20Server%20in%20the%20Cloud)


&nbsp;   
<a id="storage-model"></a>
## NSM & DSM

- [Column-Stores vs. Row-Stores - How Different Are They Really](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Column-Stores%20vs.%20Row-Stores%20-%20How%20Different%20Are%20They%20Really)


&nbsp;   
<a id="query"></a>
## Query

- [MonetDB/X100: Hyper-Pipelining Query Execution](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/MonetDB%20X100%20-%20Hyper-Pipelining%20Query%20Execution)
  - 在现代体系结构下对控制流和数据流的思考
- [Scan Primitives for Vector Computers](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Scan%20Primitives%20for%20Vector%20Computers)
- [Adaptive Execution of Compiled Queries](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Adaptive%20Execution%20of%20Compiled%20Queries)

#### Vectorization
- [Everything You Always Wanted to Know About Compiled and Vectorized Queries But Were Afraid to Ask](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Everything%20You%20Always%20Wanted%20to%20Know%20About%20Compiled%20and%20Vectorized%20Queries%20But%20Were%20Afraid%20to%20Ask)
- [A Vectorized Hash-Join](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/A%20Vectorized%20Hash-Join)
  - histogram, rank and permute
- [Vectorization vs. Compilation in Query Execution](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Vectorization%20vs.%20Compilation%20in%20Query%20Execution)
  - 向量化执行的具体细节，原论文 [Just-in-time Compilation in Vectorized Query Execution]()
- [Rethinking SIMD Vectorization for In-Memory Databases](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Rethinking%20SIMD%20Vectorization%20for%20In-Memory%20Databases)
  - 向量化执行具体细节和大量实验

#### Code Generation
- [Efficiently Compiling Efficient Query Plans for Modern Hardware](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Efficiently%20Compiling%20Efficient%20Query%20Plans%20for%20Modern%20Hardware)
  - 分析 codegen 控制流 produce/consume
- [Relaxed Operator Fusion for In-Memory Databases](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Relaxed%20Operator%20Fusion%20for%20In-Memory%20Databases)
  - 从 query tree 分割 pipeline
- [Push vs Pull-Based Loop Fusion in Query Engines](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Push%20vs%20Pull-Based%20Loop%20Fusion%20in%20Query%20Engines)

#### Join
- [Analysis of Two Existing and One New Dynamic Programming Algorithm for the Generation of Optimal Bushy Join Trees without Cross Products]() todo
- [Optimizing Main-MemoryJoin on Modern Hardware](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Optimizing%20Main-MemoryJoin%20on%20Modern%20Hardware) 构建 memory access 测量模型
- [Sort vs. Hash Revisited - Fast Join Implementation on Modern Multi-Core CPUs](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Sort%20vs.%20Hash%20Revisited%20-%20Fast%20Join%20Implementation%20on%20Modern%20Multi-Core%20CPUs)
  - hash join 和 sort merge join 的方案
- [Multi-Core, Main-Memory Joins - Sort vs. Hash Revisited](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Multi-Core%2C%20Main-Memory%20Joins%20-%20Sort%20vs.%20Hash%20Revisited)
- [Efficient Main-Memory Hash Joins on Multi-Core CPUs](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Efficient%20Main-Memory%20Hash%20Joins%20on%20Multi-Core%20CPUs)
  - 分析 hash join 的各种方案
- [Design and Evaluation of Main Memory Hash Join Algorithms for Multi-core CPUs](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Design%20and%20Evaluation%20of%20Main%20Memory%20Hash%20Join%20Algorithms%20for%20Multi-core%20CPUs)
  - no-partition hash join 值得使用，除了 cache/TLB miss 也要关注 computation 和 synchronization，实验挺丰富
- [Main-Memory Hash Joins on Multi-Core CPUs: Tuning to the Underlying Hardware](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Main-Memory%20Hash%20Joins%20on%20Multi-Core%20CPUs%20-%20Tuning%20to%20the%20Underlying%20Hardware) hash join 的各种实验
- [Improving Main Memory Hash Joins on Intel Xeon Phi Processors: An Experimental Approach](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Improving%20Main%20Memory%20Hash%20Joins%20on%20Intel%20Xeon%20Phi%20Processors%20-%20An%20Experimental%20Approach) 优化实验论文
- [Massively Parallel NUMA-aware Hash Joins](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Massively%20Parallel%20NUMA-aware%20Hash%20Joins)
- [Massively Parallel Sort-Merge Joins in Main Memory Multi-Core Database Systems](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Massively%20Parallel%20Sort-Merge%20Joins%20in%20Main%20Memory%20Multi-Core%20Database%20Systems)
  - NUMA 场景下 sort join 的细节以及实验对比（文中的 **parallel partition** 方案讲得很细）
  - 对于 **partition skew** 的处理
- [Fast Sort on CPUs and GPUs: A Case for Bandwidth Oblivious SIMD Sort](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Fast%20Sort%20on%20CPUs%20and%20GPUs%20-%20A%20Case%20for%20Bandwidth%20Oblivious%20SIMD%20Sort)
  - 详细分析了 radix sort 和 merge sort，并讨论如何利用 线程级并行 和 SIMD


&nbsp;   
<a id="index"></a>
## Index

- [Easy Lock-Free Indexing in Non-Volatile Memory](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Easy%20Lock-Free%20Indexing%20in%20Non-Volatile%20Memory)
  - persistent multi-word CAS 给 concurrent index 更好支持


&nbsp;   
<a id="cc"></a>
## Concurrency Control

- [A Critique of ANSI SQL Isolation Levels](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/A%20Critique%20of%20ANSI%20SQL%20Isolation%20Levels)
- [An Empirical Evaluation of In-Memory Multi-Version Concurrency Control](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/An%20Empirical%20Evaluation%20of%20In-Memory%20Multi-Version%20Concurrency%20Control)
- [Staring into the Abyss - An Evaluation of Concurrency Control with One Thousand Cores](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Staring%20into%20the%20Abyss%20-%20An%20Evaluation%20of%20Concurrency%20Control%20with%20One%20Thousand%20Cores)
- [Fast Serializable Multi-Version Concurrency Control for Main-Memory Database Systems](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Fast%20Serializable%20Multi-Version%20Concurrency%20Control%20for%20Main-Memory%20Database%20Systems)
- [High-Performance Concurrency Control Mechanisms for Main-Memory Databases](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/High-Performance%20Concurrency%20Control%20Mechanisms%20for%20Main-Memory%20Databases)
- [Speedy Transactions in Multicore In-Memory Databases](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Speedy%20Transactions%20in%20Multicore%20In-Memory%20Databases)
  - epoch-based group txn


&nbsp;   
<a id="buffer"></a>
## Buffer Pool

- [Anti-Caching: A New Approach to Database Management System Architecture](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Anti-Caching%20-%20A%20New%20Approach%20to%20Database%20Management%20System%20Architecture)
  - 将纵向的 dbpage fault sync fetch 改为水平化的 async fetch


&nbsp;   
<a id="recovery"></a>
## Log & Recovery

- [ARIES](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/ARIES) todo
- [Constant Time Recovery in Azure SQL Database](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Constant%20Time%20Recovery%20in%20Azure%20SQL%20Database)
- [Write-Behind Logging](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Write-Behind%20Logging)
  - DTT 不记录 after-image，使用 group commit，形成天然的 checkpoint


&nbsp;   
<a id="gc"></a>
## GC

- [Hybrid Garbage Collection for Multi-Version Concurrency Control in SAP HANA](https://github.com/rsy56640/paper-reading/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93/content/Hybrid%20Garbage%20Collection%20for%20Multi-Version%20Concurrency%20Control%20in%20SAP%20HANA)


&nbsp;   
<a id=""></a>


