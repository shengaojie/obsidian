
> [!NOTE] 作用
> 修改用户的密码


> [!NOTE] 语法
```shell
passwd [参数] 用户名


参数：
-d:  # 删除已有的密码
-l： # 锁定用户的密码值，不允许修改
-u： # 解锁用户的密码值，允许修改
-e:  # 强制用户下次登录时修改密码
```




> [!example] 
```shell
1.passwd shengaojie 
2.passwd -d shengaojie             # 删除用户的密码
3.passwd -l shengaojie             # 锁定用户的密码，不允许修改
4.passwd -u shengajie              # 解锁用户的密码允许修改
```


