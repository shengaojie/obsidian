
> [!function]
> 使用字符串替换的方式，批量的修改文件名 





> [!grammer]  Perl版本的语法
```shell
rename 's/old/new' files

old:    原先的文件名
new:    需要替换成的文件名
files:  需要改变文件名的文件列表

## 参数：
-n    模拟运行，并没有产生实际的效果
```



> [!example] 
```shell
#将myfile.txt改成myfile.doc
rename 's/.txt/.doc' myfile.txt

# 将所有的.txt结尾的文件中file,改为file0
rename 's/file/file0' *.txt
```


> [!grammer] C语言版本的语法
```shell
rename [OPTION] [表达式] [替换] [文件]

参数中的nv 最好一起使用
```


> [!example] 
```shell
# 当前目录下的所有.txt结尾的换成.doc结尾
rename .txt .doc *

# 将file替换成file0
rename file file0 file*
```


