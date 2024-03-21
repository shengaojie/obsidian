# 概念

> [!notion] 
> * string是redis最基本的类型，一个key对应一个value
> * string类型是二进制安全的，意思是redis的string可以包含任何数据，比如jpg图片或者序列化的对象 
> * string类型是Redis最基本的数据类型，一个redis中字符串value最多可以是512M
> * 单值单value



# 方法
> [!NOTE] 设置/获取键值
```shell
# 设置获取单个键值
set key value
get key value

# 先获取值在设置值
getset key value

# 设置获取多个键值
mset key1 value1 key2 value2...
mget key1 key2

# 同时设置一个或者多个键值，仅仅在所有的key都不存在时才可以
msetnx key1 value1 key2 value2 ...
```




> [!NOTE] 获取指定范围内的值
```shell
getrange
setrange
```


> [!NOTE] 数值的增减
> 首先必须要是数字才能增减
```shell
# 增加1
incr key

# 增加指定的值
incrby key increment

# 减1
decr key

# 减少指定的值
decrby key decrement
```



> [!NOTE] 追加内容和获取字符串长度
```shell
# 增加指定内容
append key value
# 获取字符串长度
strlen key
```


> [!NOTE] 分布式锁
> setex key 和set key 加上 expire key 的作用效果一样，但是前者是原子操作
```shell
# 不存在key的后才设置key和value
setnx key value
# 设置键值对，并设置持续时间
setex key seconds value
```

# 使用场景

