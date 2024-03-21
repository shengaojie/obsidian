
> [!function]
> 查看文件的尾部 




> [!grammer] 
```shell
tail [option] [FILE]

## 参数
-c:   输出文件尾部的N个字节的内容
-f:   **显示文件中新增加的内容，看日志很有用**
-n:   输出文件尾部的n行内容
```




> [!example] 
```shell
# 默认的话，是显示文件的最后10行内容
tail file.txt
# 显示文件的最后20行内容
tail -n 20 file.txt
# 从文件的第20行显示到结束
tail -n +20 file.txt
# 显示文件的最后10个字节
tail -c 10 file.txt
# 动态的显示文件新增的内容
tail -f file.txt
```




