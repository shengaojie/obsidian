
> [!function] 
> 1.移动文件  
> 2.重命名文件



> [!grammer] 
```shell
1.移动文件
mv [OPTION] source dest

2.重命名文件
mv file1.txt newFile.txt


# 参数
-i      如文件存在同名，向用户询问是否覆盖
-f      覆盖已有文件的时候，不进行任何的提示
-b      当文件存在的时候，为其创建一个备份
-u      当源文件比较新的时候，或者是目标文件不存在的时候才移动
```



> [!example] 
```shell
# 移动文件
mv file.txt dir

# 重命名
mv file.txt newFile.txt

# 重命名时询问是否覆盖,newFile.txt文件已经存在了
mv -i file.txt newFil.txt

# 文件被覆盖之前备份
mv -b file.txt file2.txt

# 源文件比较新的时候才移动
mv -u file1.txt file2.txt

# 将当前文件夹中的所有的东西移动到上一级
mv * ../

# 将一个文件夹中的内容移动到另一个文件夹中
mv dir1/* dir2
```


