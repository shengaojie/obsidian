
> [!NOTE] 作用
> 创建并且设置用户相关信息



> [!NOTE] 语法
```shell
useradd [参数] 用户名
[参数]
-m: 自动创建用的家目录
-s: 指定用户登录的shell
-d: 指定用户登入时的目录
```



> [!example] 
```shell
1.useradd user1
2.useradd -m -s /bin/bash user1     # 自动创建家目录并且指定登录的shell
3.useradd -m user1                  # 自动创建家目录
4.useradd -m -d /new/dir user1      #指定家目录的位置
```



