
> [!function] 
> 搜索指定的文件
> 


> [!grammer] 
```shell
find [路径] [条件]

## 参数
-user                              匹配所有者
-group                             匹配所有组
-perm                              匹配权限
-name                              匹配名字
-iname                             匹配名字但是会忽略大小写
-size                              匹配文件大小 （+50KB查找超过的，-50KB同理）
-mtime -n +n                       匹配修改内容的时间，单位是天
-atime -n +n                       匹配访问内容的时间，单位是天
-ctime -n +n                       匹配修改文件权限的时间，单位是天
-type b/d/c/p/l/f                  按照文件的类型匹配（块设备、目录、字符设备、管道、链接文件、文本文件）
```

> [!example] 

1. find / -name \*.conf                        找到/目录下的所有的以\*.conf结尾的文件
2. find /etc -size +1k                         在etc目录下找到文件大小约为1k的文件
3. find /home -user shengaojie       在home目录下找到shengaojie用户的文件
4. find . -iname  \*.txt                        搜索当前目录下的后缀为.txt的文件，后缀不区分大小写
5. find . ! -name \*.txt                        找到当前目录下后缀不是.txt结尾的文件
6. find . -mtime -7                            找到当前文件夹下7天修改过的文件



> [!example] 排除掉某个目录
> **注意. ! -path 之间都有空格**

```shell
//找到当前文件夹下，除了dir文件下所有以txt结尾的文件
find . ! -path './dir/*' -name "*.txt"  
```
