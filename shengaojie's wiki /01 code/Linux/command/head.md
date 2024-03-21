
> [!function] 
> 



> [!grammer] 
```shell
head [OPTION] [FILE]

## 参数
-n:   接数字表示显示的行号
-c:   接数字表示显示的字节数
```


> [!example] 
```shell
# 默认显示10行
head ~/.zshrc

# 显示五行
head -n 5 file.txt

# 显示除了倒数后6行的所有的内容
head -n -6 file.txt

# 显示20个字节
head -c 20 file.txt
```


