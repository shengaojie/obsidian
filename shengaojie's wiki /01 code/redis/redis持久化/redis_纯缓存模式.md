
> [!what] 
> 同时关闭rdb和aof



> [!how] 
> 1. 关闭RDB
> 	* 配置文件中修改为`save ""`,禁用RDB模式下我们依然可以使用`bgsave`来生产rdb文件
> 2. 关闭AOF
> 	* 配置文件中修改为`appendlyno`，禁用aof的模式之下，我们可以使用`bgrewriteaof来生成aof文件`
