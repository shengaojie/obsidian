
> [!why] 
> 有的时候Service之间也会相互调用，为了避免出现循环依赖问题，MybatisPlus提供一个静态工具类：`Db`

![[CleanShot 2024-02-26 at 16.00.35@2x.png]]
Db中的很多方法和`IService`中的签名一致，不同的地方在于因为是静态工具，所以没有泛型，需要我们参数中传入对应的class类型



> [!how] 

```java
@Test
void testDbGet() {

    User user = Db.getById(1L, User.class);
    System.out.println(user);
}

@Test
void testDbList() {
    // 利用Db实现复杂条件查询
    List<User> list = Db.lambdaQuery(User.class)
            .like(User::getUsername, "o")
            .ge(User::getBalance, 1000)
            .list();
    list.forEach(System.out::println);
}

@Test
void testDbUpdate() {
    Db.lambdaUpdate(User.class)
            .set(User::getBalance, 2000)
            .eq(User::getUsername, "Rose");
}

```
