
> [!notion] 
> * Redis 的 Set 是 [[redis_String|String]] 类型的**无序**集合。集合成员是唯一的，这就意味着集合中**不能出现重复的数据**，集合对象的编码可以是 intset 或者 hashtable。
> * Redis 中Set集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。
> * 集合中最大的成员数为 2^32 - 1 (4294967295, 每个集合可存储40多亿个成员)
> * 单值多value



> [!method] 方法
```shell
# 添加元素
sadd key member1 member2...
# 遍历所有的元素
smembers key

# 判断元素是否在集合中
sismember key member

# 获取集合中的元素个数
scard key

# 从集合中随机展示几个元素，元素不会被删除
srandmember key count
# 从集合中随机弹出几个数字，数字会被删除
spop key count

# 将集合key1中的某个值移动到key2
smove key1 key2 member

# 删除元素
srem key member1 member2 ...
```

![[CleanShot 2024-01-14 at 21.13.06@2x.png]]



> [!method] 集合运算
> 
```shell
# 属于key1，但是不属于key2的
sdiff key1 key2
# 属于key1或属于key2的
sunion key1 key2

# 属于key1也属于key2的
sinter key1 key2

# 属于key1的也属于key2的，但是不返回结果集，返回的是交集的个数
# numkeys： key的数量
# limit: 想要显示的相交元素的数量
sintercard numkeys key1 key2 ... [limit limit]
```
![[CleanShot 2024-01-15 at 09.00.20@2x.png]]

