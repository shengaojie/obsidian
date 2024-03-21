
> [!function] 
> 设置或者是显示环境变量



> [!grammer] 
```shell
export [选项] 文件

# 参数
-p:    列出所有的shell程序赋予的环境变量

```



> [!example] 
> 
```shell
# 列出所有的环境变量
export -p

# 定义环境变量
export MYENV

# 定义环境变量并且复制
export MYENV=7

# 修改环境变量PATH
export PATH=$PATH:/usr/local/mysql/bin

```
