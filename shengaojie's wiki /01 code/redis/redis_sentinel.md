
> [!what] 
> 哨兵巡查后台master主机是否故障，如果发生故障根据**投票数**自动将某一个从库转换为新的主库
> 1. 监控redis运行状态，包括master和slave
> 2. 当master down机，能自动将slave切换成新master


> [!why] 为什么需要哨兵？
> 原先的主从模式在master宕机之后，不能自动重新选择一个master，需要认为干预



> [!NOTE] 重点参数说明
> 1. `sentinel monitor <master-name> <ip> <redis-port> <quorum>`：设置要监控master的ip和端口，其中的quorum表示最少几个哨兵主观认为下线同意故障迁移
> 2. `sentinel auth-pass <master-name> <passwd> `: master可能设置了密码，连接master机器的密码
> 3. daemonize：表示是否已后台方式启动
> 



> [!NOTE] 哨兵的运行的流程和执行原理
1. 三个哨兵监控，一主二从并且处于正常运行的状态下
![[CleanShot 2024-01-23 at 09.35.39@2x.png|500]]
2. `SDwon`（Subjectively Down）主观下线
	* 表示单个`sentinel`自己主观上检测到master的状态，从`sentinel`的角度上来看，如果发送了ping心跳包之后，一定的时间内如果没有收到合法的回复，就认为是达到了`SDown`的条件。
	* `sentinel down-after-milliseconds <masterName> <timeout>`,这个配置就是关于主观认为下线的依据，默认是30s。意思是如果30s内如果`sentinel`没有收到master的回复的话，这个`sentinel`就可以客观的认为这个master下线了
3. `ODown`（Objective Down）：当多个`sentinel`达成一致的意见认为一个master已经宕机了，就认为主观认为这个master已经下线了
4. 选举出哨兵中的`leader`
	* 当主节点被客观认为下线之后，各个哨兵节点会进行协商，选举出一个哨兵中的`leader`。并且由该`leader`进行故障迁移。其中使用的是Raft算法
5. 故障迁移的流程
	* 某个slave被选成新的master(**新主登基**)
		* 选举成为新的master的规则
			* `redis.conf`文件中的`slave-priority`或者是`replica-priority`的优先级的设置，越小优先级越高
			* 复制偏移位置offset最大的节点
	* 重新拜码头（**群臣俯首**）
		* 让被选中的节点成为master的节点
		* `leader`让新的master节点执行`slaveof no one`
		* `leader`让别的节点执行`slaveof`让别的节点成为新master的子节点
	* 老的master回来也要俯首称臣 （**旧主拜服**）
		* 如果此时老的master重新回归，`leader`会将其降级为slave,并回复正常工作



> [!example] 
> 说明：
> * 三台机器，一台作为master，两台作为slave，其中的三个哨兵配置在master机器上。端口分别为：26379,26380,26381
> * 哨兵的启动方式：`redis-sentinel sentinel26379.conf --sentinel`
> * 流程：
> 	1. 先启动三台机器，查看是否能正常进行主从复制
> 	2. 启动三台哨兵
> 	3. 将原先的master宕机
> 		*  查看此时的主从关系的变化
> 	4. 将原先的master重新连接
> 		* 查看此时的主从关系



> [!NOTE] sentinel.log的变化
![[CleanShot 2024-01-23 at 11.18.43@2x.png]]


> [!NOTE] 当Master-slave切换之后
> * master.redis.conf,slave.redis.conf,sentinel.conf文件都会发生变化
> * 其中的sentinel.conf文件的监控目标会发生改变
> * 原先的master.redis.conf文件的最后会新增配置
> 	`replicaof 10.211.55.8 6381`
> 


```shell
# 哨兵sentinel.conf配置
bind 0.0.0.0
daemonize yes
protected-mode no
port 26379
logfile "/myredis/sentinel26379.log"
pidfile /var/run/redis-sentinel26379.pid
dir /myredis
sentinel monitor mymaster 192.168.111.169 6379 2
sentinel auth-pass mymaster 111111
```


> [!question] master宕机之后
> 当master宕机之后，如果此时使用`info replication`查看主从关系，会出现错误。意思是原先的管道已经断开了 ，可以再次输入命令，等待重新建立连接之后即可。
> 


> [!attention] 注意
> 作为master机器的redis.conf文件中需要配置masterauth选项，否在在master宕机后，后续可能会变成从机，需要设置访问新主机的密码，否则可能会报错*master_link_status:down*


