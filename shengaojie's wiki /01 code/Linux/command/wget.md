
> [!function] 
> 文件下载



> [!grammer] 
```shell
wget [option] [URL]

# 参数
-i:      通过文件中的下载地址下载
-O:      下载后重命名文件
-c:      打开断点续传（如果下载中断了，下次重新下载的时候是从上次下载到的位置）
-b:      后台下载
-p:      指定保存路径
```


> [!example] 
```shell
# 下载单个文件
wget https://cn.wordpress.org/latest-zh_ CN.zip

# 下载多个文件
wget -i urllsit.txt
# 下载后的文件重命名
wget -O wp.zip https://cn.wordpress.org/ latest-zh_CN.zip

# 下载后保存在指定的目录
wget -P dir https://cn.wordpress.org/latest- zh_CN.zip

# 断点续传
wget -c https://cn.wordpress.org/latest-zh_ CN.zip

# 后台下载，并且查看下载进度
wget -b https://cn.wordpress.org/latest-zh_ CN.zip
tail -f wget -log
```

