
> [!notion] 
> 同时开启rdb和aof
> * 开启方式：修改`aof-use-rdb-preamble yes` 为 yes
> 


> [!question] 同时开启两种的执行流程
> ![[CleanShot 2024-01-18 at 15.30.34@2x.png]]




> [!principle]  RDB镜像做全量持久化，AOF做增量持久化
> * 先使用RDB进行快照存储
> * 然后使用AOF持久化记录所有的写操作
> * 当重写策略满足或手动触发重写的时候，将最新的数据存储为新的RDB记录。这样的话，重启服务的时候会从RDB和AOF两部分恢复数据，既保证了数据完整性，又提高了恢复数据的性能。简单来说：混合持久化方式产生的文件一部分是RDB格式，一部分是AOF格式。**----》AOF包括了RDB头部+AOF混写**
> ![[CleanShot 2024-01-18 at 15.36.51@2x.png]]
