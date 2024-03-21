
> [!notion] 
> Redis GEO 主要用于存储地理位置信息，并对存储的信息进行操作，包括
> * 添加地理位置的坐标
> * 获取地理位置的坐标
> * 计算两个位置之间的距离
> * 根据用户给定的经纬度坐标来获取指定范围内的地理位置集合




> [!method] 
> 使用[[redis_zset|zrange]]可以查看所有的元素
```shell
geoadd
# 返回键里所有的元素
geopos

# 返回两个元素之间的距离
geodist
# 以给定的经度和纬度为中心，返回不超过给定距离的所有元素
georadius

# 和georadius类似
georadiusbymember

# 返回一个或者是多个元素位置的hash表示
geohash
```
![[CleanShot 2024-01-17 at 10.51.31@2x.png]]


> [!question] 中文乱码问题？
> 1. 先使用quit退出客户端  
> 2. 使用该命令重新登录：redis-cli -a 5243 --raw



  


