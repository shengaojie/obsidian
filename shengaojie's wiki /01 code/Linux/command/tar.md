
> [!function] 
> 打包/解压工具


```shell
# 参数
-c        新建打包文件
-x        解压文件
-f        指定要处理的文件的
-v        显示过程
-z        通过gzip的方式解压或者压缩，最后是.tar.gz为后缀
-t        查看包中的内容
-C        指定解压或者是压缩的目录，如果没有的话，默认是当前包中
```




> [!example] 
```shell
tar -cvf file.tar *.txt        当前包下的所有txt文件打包成file.tar,没有压缩
tar -zcvf file.tar.gz *.txt       当前包下的txt文件打包成file.tar.gz并且压缩
tar -zxvf file.tar.gz          解压file.tar.gz到当前的目录中
tar -zxvf file.tar.gz -C dir/  解压file.tar.gz到当前目录的dir文件夹中
tar -tf file.tar.gz            查看压缩包中的内容
```

