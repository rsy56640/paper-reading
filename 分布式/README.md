# Record Distributed System Papers Reading

- [Distributed Database](#distributed_database)
- [Distributed Computing](#distributed_computing)
- []()



TODO:

- Bigtable
- Chubby
- Dremel
- GFS
- Haystack
- Mapreduce
- Percolator
- Raft
- Spinnaker
- Zk


&nbsp;   
<a id="distributed_database"></a>
## Distributed Database

- [Spanner](https://github.com/rsy56640/paper-reading/tree/master/%E5%88%86%E5%B8%83%E5%BC%8F/content/Spanner)
- [No Compromises - Distributed Transactions with Consistency, Availability, and Performance](https://github.com/rsy56640/paper-reading/tree/master/%E5%88%86%E5%B8%83%E5%BC%8F/content/No%20Compromises%20-%20Distributed%20Transactions%20with%20Consistency%2C%20Availability%2C%20and%20Performance)
  - FaRM V1，不需要使用全局时间戳，concurrent validation
- [Fast General Distributed Transactions with Opacity](https://github.com/rsy56640/paper-reading/tree/master/%E5%88%86%E5%B8%83%E5%BC%8F/content/Fast%20General%20Distributed%20Transactions%20with%20Opacity)
  - FaRM V2，相比 V1，加入了时钟同步，因此有了 Multi-Version
  - 没有说明 index 怎么搞，这是一个难点
- [Using One-Sided RDMA Reads to Build a Fast, CPU-Efficient Key-Value Store](https://github.com/rsy56640/paper-reading/tree/master/%E5%88%86%E5%B8%83%E5%BC%8F/content/Using%20One-Sided%20RDMA%20Reads%20to%20Build%20a%20Fast%2C%20CPU-Efficient%20Key-Value%20Store)
  -  考虑没有索引，或者简单索引
- [Fast In-memory Transaction Processing using RDMA and HTM](https://github.com/rsy56640/paper-reading/tree/master/%E5%88%86%E5%B8%83%E5%BC%8F/content/Fast%20In-memory%20Transaction%20Processing%20using%20RDMA%20and%20HTM)
  - 使用 HTM 的一个原因居然是 RDMA CAS 与 local CAS 不兼容
  - 使用 expired time 作为 shared lock
- [Fast and General Distributed Transactions using RDMA and HTM](https://github.com/rsy56640/paper-reading/tree/master/%E5%88%86%E5%B8%83%E5%BC%8F/content/Fast%20and%20General%20Distributed%20Transactions%20using%20RDMA%20and%20HTM)
  - distributed transaction 和 FaRM V1 类似，使用 HTM 替代了 local write lock，但是要补上 remote read lock
  - index 是每个存储节点自己维护，对外提供 KV 接口



&nbsp;   
<a id="distributed_computing"></a>
## Distributed Computing