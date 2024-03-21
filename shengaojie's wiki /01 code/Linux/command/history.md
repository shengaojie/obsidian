
> [!function]
> 显示和管理历史命令记录 



> [!grammer] 
```shell
history [参数]

## 参数
-c  清空历史名利
-d  删除指定序号的历史命令
-n  读取命令记录
```


> [!example] 
```shell
# 查看所有的命令记录
history
# 显示执行过的最近的五条
history 5

# 重新执行2039命令
!2039

# 重新执行上一条命令
!!

# 删除特定的命令
history -d 1234

# 清空所有的历史记录
history -c
```

