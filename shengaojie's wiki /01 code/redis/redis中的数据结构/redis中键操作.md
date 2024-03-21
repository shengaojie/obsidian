
```shell
keys *             # 查看当前库中的所有的key
exists key         # 判断某个key是否存在
type key           # 查看某个key的类型
expire key 秒钟     # 设置key的过期时间
ttl key            # 查看某个key的过期时间
del key            # 删除某个key
unlink key         # 非阻塞的删除某个key
select dbindex     # 选择某个库
move key dbindex[0-15]   # 将某个key移动到某个库中
fulshdb            # 清空当前的库
flushall           # 通杀所有的库
```