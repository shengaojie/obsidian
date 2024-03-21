
> [!what]
> 来代替`mybatis`中的`<where></where>`标签，对于单表查询不用写复杂的sql，而是通过条件构造器来构成符合要求的sql

![[CleanShot 2024-02-25 at 19.53.25@2x.png]]
`Wrapper`的子类`AbstractWrapper`提供了where中包含的所有条件构造方法：
![[CleanShot 2024-02-25 at 20.02.11@2x.png]]

而QueryWrapper在AbstractWrapper的基础上拓展了一个select方法，允许指定查询字段：
![[CleanShot 2024-02-25 at 20.02.44@2x.png]]

UpdateWrapper在AbstractWrapper的基础上拓展了一个set方法，允许指定SQL中的SET部分：
![[CleanShot 2024-02-25 at 20.02.58@2x.png]]



> [!NOTE] 基于QueryWrapper的查询
>**无论是修改、删除、查询，都可以使用QueryWrapper来构建查询条件 **

1. 查询出名字中带有o的，并且存款大于1000的人
```java
// 1.构建查询条件  
QueryWrapper<User> wrapper = new QueryWrapper<User>()  
					.select("id", "username", "info", "balance")  
					.like("username", "o")  
					.ge("balance", 1000);  
// 2.查询  
List<User> users = userMapper.selectList(wrapper);

```


2. 更新用户名为jack的用户的余额为2000
```java
// 1.要更新的数据  
User user = new User();  
user.setBalance(2000);  
// 2.更新的条件  
QueryWrapper<User> wrapper = new QueryWrapper<User>().eq("username", "jack");  
// 3.执行更新  
userMapper.update(user,wrapper);
```



> [!NOTE] UpdateWrapper
1. 能解决什么问题？
BaseMapper中的update方法更新时只能直接赋值，但是如果想要实现如下的需求：
更新id为`1,2,4`的用户的余额，扣200，对应的SQL应该是
```sql
update user set balance = balance - 200 where id in (1,2,4)
```
这个使用需要使用到setSql功能

```java
@Test  
void testUpdateWrapper() {  
	List<Long> ids = List.of(1L, 2L, 4L);  
	UpdateWrapper<User> wrapper = new UpdateWrapper<User>()  
			.setSql("balance = balance - 200")  
			.in("id", ids);  
	userMapper.update(null, wrapper);  
}
```




> [!NOTE]  LambdaQueryWrapper、LambdaUpdateWrapper

1. 为什么需要LambdaQueryWrapper？
因为无论是使用`QueryWrapper`还是`UpdateWrapper`在构造条件的时候都需要写死字段名称。
有一种解决问题的方法是，使用基于变量的`getter`方法结合反射技术，我们只需要提供给mp对应字段的`getter`方法即可。

```java
void testLambdaQueryWrapper() {  
	// 1.构建查询条件  
	LambdaQueryWrapper<User> wrapper = new LambdaQueryWrapper<User>()  
		.select(User::getId, User::getUsername, User::getInfo,         User::getBalance)  
		.like(User::getUsername, "o")  
		.ge(User::getBalance, 1000);  
	// 2.查询  
	List<User> users = userMapper.selectList(wrapper);  
	users.forEach(System.out::println);  
}
```

