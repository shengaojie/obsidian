# 概念

> [!notion] 
> * 一个双端链表的结构，容量是2的32次方减1个元素，大概40多亿，主要功能有push/pop等，一般用在栈、队列、消息队列等场景。
> * left、right都可以插入添加
> * 如果键不存在，创建新的链表；如果键已存在，新增内容；如果值全移除，对应的键也就消失了
> * 单key多value
> * 它的底层实际是个**双向链表，对两端的操作性能很高，通过索引下标的操作中间的节点性能会较差。**
> 	![[CleanShot 2024-01-14 at 19.41.55@2x.png]]




# 方法
> [!NOTE] 添加
```shell
# 从左边推入
lpush

# 从右边推入
rpush

# 在某个元素的前后插入新的值
linsert key before/after old new
```


> [!NOTE] 删除
```shell
lrem key count value     # 删除num个值等于value的元素

# 表示从list中删除3个k1,因为list中可能会存在多个相同的值
lrem list1 3 k1 
```


> [!NOTE] 修改
```shell
# 修改某一个位置的值
lset key index value
```



> [!NOTE] 获取值/遍历
```shell
lrange key 0 -1
lrange key start end

# 获取指定位置的值
lindex key index

# 从左边弹出值
lpop
# 从右边弹出值
rpop

# 从而一个列表的👉🏻弹出一个值，将该值插入到另一个列表的👈🏻
rpoplpush source dest

# 截取指定的范围
ltrim key start end
```
![[CleanShot 2024-01-14 at 20.01.13@2x.png]]




