
> [!function]
> 文本搜索工具 





> [!grammer] 
```shell
grep [参数] 文件

# 参数：
-i       忽略大小写
-c       值输出匹配的行的数量
-n       显示所有的匹配的行，并且显示行号
-h       查询多文件时，不显示文件名
-v       显示不含有匹配信息的行
-r       递归搜素
-l       只显示匹配的文件名，不显示匹配到行号
```



> [!example] 
```shell
# 搜索某个文件中的关键词
grep love file1.txt

# 搜索多个文件中的关键词
grep love file1.txt file2.txt

# 搜索关键词，但是不先文件名称
grep -h love file.txt file1.txt

# 递归搜索
grep -r love dir1/ file1.txt

# 反向查找，不匹配的行
grep -v love file1.txt

# 只显示文件名，不先匹配到的行号
grep -l love file.txt


```


