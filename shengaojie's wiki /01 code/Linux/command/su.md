
> [!function] 
> 切换用户身份


> [!grammer] 
```shell
su [参数] 用户名
# 参数
-c     执行完指令之后，恢复原来的身份
-      完全变更身份（也改变工作目录）
```



> [!example] 
```shell
su        切换为root用户
su -c whoami shengaojie   切换到shengaojie用户并且执行whoami指令之后返回
su shengaojie     切换到shengaojie，不改变工作目录
su - shengaojie   切换到shengaojie，并且改变工作目录   
```


