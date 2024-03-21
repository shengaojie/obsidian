
> [!function] 
> 包管理器，可以认为apt是apt-get的替代。是Debian系列Linux发行版中常用的包管理工具


> [!grammer] 
```shell
apt 选项 软件包
```



> [!example] 
```shell
# 列出所有需要更新的软件包
sudo apt update

# 更新所有可以更新的软件包
sudo apt upgrade
# 更新某一个具体的软件包
sudo apt upgrade xxx

# 安装某一个具体的软件包
sudo apt install xxx

# 删除某一个软件包
sudo apt remove xxx
# 清理不在使用的依赖或者库文件
sudo apt autoremove
# 列出已经安装的所有的软件包
sudo apt list --installed
```


