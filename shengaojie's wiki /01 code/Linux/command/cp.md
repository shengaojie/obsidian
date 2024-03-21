
> [!function] 
> 复制文件或者是目录





> [!grammer] 
```shell
cp [OPTION] source dest

# 参数
-i      如文件存在同名，向用户询问是否覆盖
-f      覆盖已有文件的时候，不进行任何的提示
-b      当文件存在的时候，为其创建一个备份
-v      显示执行的过程
-r      递归的复制目录和文件
```



> [!example] 
```shell
# 复制文件
cp file1.txt file2.txt

# 复制目录
cp -r dir1/ dir2

# 复制文件如果已经存在，则备份
cp -b file1.txt file2.txt

# 复制文件若已经存在则询问是否覆盖
cp -i file1.txt file2.txt
```


