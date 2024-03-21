
> [!notion] 
> 在[[redis_set|set]]的基础上，每个value值的前面加上了一个score分数  
> set v1 v2 v3  
> zset score1 v1 score2 v2 score3 v3



> [!method] 
> 
```shell
zadd key score member [score member...]
# 按照分数从小到大排序，返回start到end之间的所有的元素
zrange key start end [withscores] 
# 逆向排序
zrevrange key start end [withscores] 

# 获取指定范围内的元素
# ( 表示不包含
# limit：对于返回数据的限制
# offset：开始的下标
# count：偏移量
zrangebysocre key min max [withscores] [limit offset count]

# 获取元素的分数
zscore key member
# 获取元素的数量
zcard key

# 某个socre对应的value的值，作用是删除元素
zrem key member

# 增加某个元素的分数
zincrby key increment member

# 获取指定分数范围内的元素的个数
zcount key min max

# 从排序集中弹出第一个非空的元素，它是成员分数对
zmpop numkeys key [key...] MIN|MAX [COUNT count]

# 获取下标值
zrank key values

# 获取下标值的逆序
zrevrank key values
```

![[CleanShot 2024-01-17 at 09.27.06@2x.png]]
