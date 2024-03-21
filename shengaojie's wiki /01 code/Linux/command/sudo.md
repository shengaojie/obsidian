
> [!function] 
> 以系统管理员的身份执行指令



> [!grammer] 
```shell
sudo [参数]

#参数
-l      显示当前用户的权限
-u      以指定用户的身份去执行命令，如果没有-u就是默认为root身份去执行
```


> [!NOTE] 配置文件
> 在/etc/sudoers中




> [!example] 
```shell
sudo -l       列出当前用户的权限
sudo -u shengaojie whoami   以shengaojie的身份运行whoami
sudo !!        以root的身份执行上一条命令
```


