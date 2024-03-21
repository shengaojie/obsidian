
> [!function]
> 远程连接工具

> [!Grammer] 
```shell
ssh [参数] [主机]

## 参数
-l:     指定远程连接服务器的用户名
-p:     指定远程连接服务器的端口
```



> [!example] 
```shell
##通过shengaojie用户登录主机
ssh -l shengaojie 192.168.1.126
ssh shengaojie@192.168.1.126

## 指定端口和用户登录主机
ssh -p 2222 shengaojie@192.168.1.126
```
