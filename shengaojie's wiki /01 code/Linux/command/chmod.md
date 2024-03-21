

> [!function] 
> 修改文件或者是目录的权限



> [!grammer] 
```shell
方式1：符号模式
[guoa][+-=][rwx]  

+:      添加某一项权限  
-：      去除某一项权限  
=:      设置为所给定的权限  
```

![[CleanShot 2024-01-07 at 16.55.57@2x.png]]


> [!example] 
```shell
chmod a+r file.txt            # 给所有的用户添加读的权限
chmod -R a+r *             # 当前目录下的所有的文件文件设置为可读，-R表示递归所有文件
chmod a+r,a+w,a+x file.txt   # file.txt文件设置为所有人可读，可写，可执行
```




```shell
方式2： 数字模式
```
![[CleanShot 2024-01-07 at 16.54.17@2x.png]]
> [!example] 
```shell
chmod 777 file.txt       # file.txt文件设置为所有人可读，可写，可执行
chmod 755 file.txt       # file.txt文件的持有者所有读写执行权限，其余的人只有读和执行的权限
```
