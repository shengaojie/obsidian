
> [!notion] 
> * 用String类型作为底层数据结构实现的一种统计二值状态的数据类型。位图本质是数组，它是基于String数据类型的按位的操作。该数组由多个二进制位组成，每个二进制位都对应一个偏移量(我们称之为一个索引)。
> * Bitmap支持的最大位数是2^32位，它可以极大的节约存储空间，使用512M内存就可以存储多达42.9亿的字节信息(2^32 = 4294967296)
![[CleanShot 2024-01-17 at 09.31.20@2x.png]]


> [!method] 
```shell

# offset： 表示偏移量
# value: 只能为0或者是1
setbit key offset value 

# 获取指定key，的指定偏移量处的value值
getbit key offset

# 统计长度
strlen key
# 统计一个key中含有多少个1
bitcount key

```
![[CleanShot 2024-01-17 at 10.00.52@2x.png]]

> [!question]  统计一个人一年365天登录信息，需要占用多少字节？
```shell
setbit 2023 0 1
setbit 2023 364 1
strlen 2023

# 显示结果为46
46 * 8 = 368
```
>




> [!example] 使用场景
> 1. 用户今天是否登录过
> 2. 电视、视频等是否被播放过
> 3. 打卡签到
