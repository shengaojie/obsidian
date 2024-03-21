
> [!what] 
> 两者都是为了拼写sql语句

**#{}**：先编译sql语句，再给占位符传值，底层是PreparedStatement实现。可以防止sql注入，比较常用。**本质上是占位符**

**${}**：先进行sql语句拼接，然后再编译sql语句，底层是Statement实现。存在sql注入现象。只有在需要进行sql语句关键字拼接的情况下才会用到。**本质上是字符串拼接**

能使用#{}的场合就不用使用${}



> [!NOTE] 需要使用${}的场合

1. 当需要使用关键字、表名的时候，必须要使用${}
![[CleanShot 2024-02-26 at 09.34.48@2x.png]]
因为`desc`和`asc`是一个关键字，所以一定不能带有引号，必须要使用${}

2. 批量删除
一般而言批量删除对应的sql语句为:
```sql
delete from user where id in(1,2,3);

or

delete from user where id = 1 or id = 2 or id = 3

```

```xml
<delete id="deleteByIds">  
	delete from user where id in (${ids})  
</delete>
```


3. 模糊查询
* 使用#{}
```xml
"%"#{}"%"
```
* 使用${}
```xml
'%${}%'
```
* 使用concat
```xml
concat('%',#{},'%')
```