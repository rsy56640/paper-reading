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



&nbsp;   
<a id="distributed_computing"></a>
## Distributed Computing