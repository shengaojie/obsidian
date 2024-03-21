
> [!function] 
> 作用远程拷贝文件




> [!grammer] 
> 
```shell
#远程拷贝文件
scp username@192.168.1.126:source target

source：远程文件所在的位置
target：传输到本机的位置

#远程上传文件
scp source username@10.211.55.7:target 

source：本地文件所在的位置
target：要传输到远程主机的文件位置


## 参数
-r:      递归复制整个目录
-p:      指定文件传输的端口号
```


> [!example] 
```shell
# 从远程复制文件到本地 ~
scp shengaojie@192.168.1.126:/Users/shengaojie/file.txt ~
scp -r shengaojie@192.168.1.126:/Users/shengaojie/code ~

# 上传本地文件到远程服务器
scp ~/file.txt shengaojie@10.211.55.7:/home/shengaojie/code/linux
```
