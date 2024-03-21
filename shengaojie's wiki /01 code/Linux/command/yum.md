
> [!function] 
> 是Centos中shell前端软件的包管理器,能够从指定的服务器下载RPM包并且安装,**可以自动处理依赖关系,并且一次安装所有的依赖包**,类似于java中的maven。




> [!grammer] 
```shell
yum [OPTION] 参数

# OPTION
-y        对有所的回答都是回答“yes”

# 参数
install          安装rpm软件包
update           更新rpm软件包
check-update     检查是否可以更新的rpm软件包
remove           删除指定的软件包
list             显示软件包信息
clean            清理过期缓存
```



> [!example] 
```shell
# 安装firefox
yum -y install firefox
```




> [!NOTE] 修改YUM源
> 因为默认的YUM源在国外，可以通过修改关联的网络YUM源为国内的镜像网站，如网易163和aliyun等。

1. 安装wget，使用wget来从指定的url下载文件
```
yum install wget
```
2. 下载aliyun的repos文件
```shell
wget http://mirrors.aliyun.com/repo/Centos-7.repo
```
3. 备份/etc/yum.repos.d 文件
```shell
cp Centos-Base.repo Centos-Base.repo.backup
```
4. 使用下载好的repos文件替换默认的repos文件
5. 清理旧的缓存数据，缓存新的数据
```shell
yum clean all
yum makecache    # 将服务器的包信息下载到本机缓存起来
```
6. 测试
```shell
yum list | grep firefox
yum -y install firefox
```

