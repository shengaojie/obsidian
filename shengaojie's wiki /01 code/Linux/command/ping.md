
> [!function] Title
> 测试主机之间的连通性



> [!grammer]
```shell
ping [参数] 目标主机

## 参数
-c:   指定发送报文的次数
-i:   指定发送的时间间隔

```



> [!example] 
> 
```shell
# 测试连通性
ping www.baidu.com

# 连续ping 4次
ping -c 4 www.baidu.com

# 连续ping 4次，每次间隔3s
ping -c -i 3 www.baidu.com

```