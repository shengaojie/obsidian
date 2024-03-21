
> [!notion] 
> * Redis hash 是一个 [[redis_String|string]] 类型的 field（字段） 和 value（值） 的映射表，hash 特别适合用于存储对象。
> * Redis 中每个 hash 可以存储 2^32 - 1 键值对（40多亿）
> * KV模式不变，但是V变成了一个键值对



> [!NOTE] 方法
```shell
hset 
hget
hmget
# 获取所有的值
hgetall
# 不存在key就设置
hsetnx
# 获取所有的key
hkeys
# 获取所有的value
hvals

# 在key中是否存在某个filed
hexist key file

# 某个key中filed中对应的value，增加相应的值
hincrby key field increment
## 获取某个key内的全部数量
hlen
```

![[CleanShot 2024-01-14 at 20.48.54@2x.png]]
![[CleanShot 2024-01-14 at 20.49.08@2x.png]]