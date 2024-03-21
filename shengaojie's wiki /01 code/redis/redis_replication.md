
> [!notion] 
>  为了减少单个redis的压力，将redis的读写分离。master为主机负责写，slave为从机负责读



> [!NOTE] 
> 1. 当master的数据发生变化的时候，自动会将数据同步到slave
> 2. 当slave宕机后，如果再次连上master作为他的slave，会将master中的所有的数据完整的同步到自己
> 3. 配置从库，不需要配置主库
> 4. 如果master配置了`requirepass`参数，需要密码登录。那么在slave连接`master`的时候就需要配置`masterauth`来设置密码的校验，值就是master的密码。



> [!NOTE] 相关的操作命令
>* `info replication`: 可以查看对应的主机的主从关系
>* `replicaof masterIP masterPort`：通过配置文件的方法，配置从机的master信息，每次从机宕机后，会自动找到该master作为主机，**认大哥**
>*  `slaveof masterIP masterPort`:
>	* 每次和master断开之后都需要重新连接
>	* 在运行期间执行该命令是，如果该数据库已经是某个master的从数据库了，那么会停止和远master的同步关系，转而和新的master同步，**重新拜码头**
>* `slaveof no one`: 使当前数据库停止与其他数据库的同步，**转成master，自立门户**
> 



> [!NOTE] 工作流程
> 1. slave启动成功连接到master后会发送一个sync命令，**连接成功后会做一次全量复制，slave自身原有的数据会被master数据覆盖清除** 
> 2. master节点收到sync命令后会开始在后台保存快照，同时将收集所有接受到的用于修改数据集命令缓存起来，master的节点持久化完毕之后，将rdb文件和缓存中的命令发送个slave，**完全一次全量的复制**。
> 3. `repl-ping-replica-period 10`: master每10s发出ping命令
> 4. master继续讲所有收集到的修改命令依次传递给slave
> 5. 从机下线后，如果再次重新连接，master会将从机内所缺的部分数据同步过去


> [!NOTE] 修改配置文件
> 1. 开启`daemonize yes`
> 2. 注释掉 `bind 127.0.0.1`
> 3. `protected-mode no`
> 4. 指定端口
> 5. 指定当前工作目录
> 6. pid文件的名字,`pidfile /var/run/redis_6479.pid`
> 7. logfile文件的名字，`/xxx/6379.log`
> 8. requirepass, `requirepass 5243`
> 9. dump.rdb名字，`dbfilename dump6379.rdb`
> 10. aof文件(可选)
> 11. 从机访问主机的同性密码masterauth,`masterauth 5243`



> [!advantage] 
> # 优点：
> * 读写分离
> * 容灾恢复
> * 数据备份
> * 水平扩容支持高并发
> # 缺点
> * 默认情况下，如果master宕机的话，不会从slave节点中选择一个作为master。所以每次都需要人工干预


> [!example] 主从复制的演示
> 1. 需要三个虚拟机，两个作为slave，一个作为master
> 2. 三个虚拟机之间需要两两能够ping通
> 3. 可以在配置文件中配置（永久的），也可以使用`slave of`命令（宕机之后就会失去联系）。

![[CleanShot 2024-01-19 at 10.37.38@2x.png|475]]
![[CleanShot 2024-01-19 at 10.38.22@2x.png|475]]


> [!question] 
> 1. 保持连接的过程中，如果有一个slave宕机，此时master还在持续写入，宕机的slave再次连接上后还能有这段时间内写入master的数据吗
> 	![[CleanShot 2024-01-19 at 10.47.09@2x.png]]
> 2. master宕机之后，从机会上位吗？  
> 	不会
> 3. 主机宕机之后，重启主机，之前的主从关系还在吗？  
> 	还在




> [!example] 薪火相传slaveof
> * 上一个slave可以上下一个slave的master
> * 会清除之前的数据，重新建立拷贝

![[CleanShot 2024-01-19 at 11.01.19@2x 1.png]]



> [!example] 反客为主slaveof no one

![[CleanShot 2024-01-19 at 14.11.59@2x.png]]





