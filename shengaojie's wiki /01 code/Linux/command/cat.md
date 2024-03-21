> [!function] 
> 在终端上显示文件的内容





> [!grammer] 
```shell
cat [OPTION] [FILE]

## 参数
-n  显示行号(空行也编号)
-s  去除重复的行
-b  显示行号（空行不编号）

```



> [!example] 
```shell
cat file.txt

# 查看多个文件的内容
cat file.txt file1.txt

# 查看文件的内容，并且显示行号
cat -n file.txt

# 去除重复的行
cat -s file.txt

# 重定向到文件中
cat file.txt > file1.txt
# 追加到文件中
cat file.txt >> file1.txt

# 合并成一个文件
cat file.txt file1.txt > one.txt
```


