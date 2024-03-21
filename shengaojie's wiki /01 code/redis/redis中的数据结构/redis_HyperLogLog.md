
> [!what] 
> * 一种数据集，统计去重复后的真实个数
> * `HyperLogLog` 的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定且是很小的。
> * 每个 ``HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基 数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比
> * `HyperLogLog` **只会根据输入元素来计算基数，而不会储存输入元素本身**，所以 `HyperLogLog` 不能像集合那样，返回输入的各个元素




> [!how]
```shell
# 添加元素
pfadd key element [element...]

# 返回给定的key的基数估计值
pfcount key [key...]
# 将多个key合并成一个key
pfmerge destkey sourcekey [sourcekey...]
```



> [!example]  使用场景
> 1. 统计某个网站的UV，UV就是独立的访客数量，一般是客户端ip
> 2. 用户搜索某个网站的关键词数量
> 3. 统计用户每天搜索的不同词条数
