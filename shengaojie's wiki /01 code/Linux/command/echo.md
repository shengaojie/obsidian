
> [!function] 
> 在终端输出字符串


> [!grammer] 
```shell
 echo [option] [STRING]
```




> [!example] 
```shell
# 输出字符串hello world
echo "hello world"

# 提取变量$PATH的值
echo $PATH

# 取消转义
echo $PATH

# 输出结果重定向到文件
echo "hello world" > file.txt

# 输出结果追加到文件中,上面的重定向会覆盖原文件的内容
echo "hello world" >> file.txt

# 显示命令的执行结果
echo `date`

# 输出带有换行符的内容
echo -e "a\nb\nc"
```

