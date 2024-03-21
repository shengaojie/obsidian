
> [!what] 
> MybatisPlus不仅提供了BaseMapper，还提供了通用的Service接口及默认实现，封装了一些常用的service模板方法。 通用接口为`IService`，默认实现为`ServiceImpl`，其中封装的方法可以分为以下几类：
> * save：新增
> * remove：删除
> * update：更新
> * get： 查询单个结果
> * list： 查询集合
> * count：计数
> * page：分页查询



> [!how] 
> 由于`Service`中经常需要定义与业务有关的自定义方法，因此我们不能直接使用`IService`，而是自定义`Service`接口，然后继承`IService`以拓展方法。同时，让自定义的`Service实现类`继承`ServiceImpl`，这样就不用自己实现`IService`中的接口了。

1. 定义`IUserService`继承`IService`
```java
public interface IUserService extends IService<User> { // 拓展自定义方法 

}

```

2. 编写`UserServiceImpl`,继承`ServiceImpl`,实现`IUserService`
```java
@Service 
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements IUserService {

}
```




> [!paragraph] Lambda
> Service中还提供了Lambda功能来简化我们的复杂查询及更新功能

1. 案例一：实现一个根据复杂条件查询用户的接口，查询条件如下：
- name：用户名关键字，可以为空
- status：用户状态，可以为空
- minBalance：最小余额，可以为空
- maxBalance：最大余额，可以为空
    
可以理解成一个用户的后台管理界面，管理员可以自己选择条件来筛选用户，因此上述条件不一定存在，需要做判断。

a. 定义一个接受查询条件的实体类`UserQuery`
```java
package com.itheima.mp.domain.query;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;
import lombok.Data;

@Data
@ApiModel(description = "用户查询条件实体")
public class UserQuery {
    @ApiModelProperty("用户名关键字")
    private String name;
    @ApiModelProperty("用户状态：1-正常，2-冻结")
    private Integer status;
    @ApiModelProperty("余额最小值")
    private Integer minBalance;
    @ApiModelProperty("余额最大值")
    private Integer maxBalance;
}
```

b. 定义一个UserController中的方法

```java
@GetMapping("/list")
@ApiOperation("根据id集合查询用户")
public List<UserVO> queryUsers(UserQuery query){
    // 1.组织条件
    String username = query.getName();
    Integer status = query.getStatus();
    Integer minBalance = query.getMinBalance();
    Integer maxBalance = query.getMaxBalance();
    // 2.查询用户
    List<User> users = userService.lambdaQuery()
            .like(username != null, User::getUsername, username)
            .eq(status != null, User::getStatus, status)
            .ge(minBalance != null, User::getBalance, minBalance)
            .le(maxBalance != null, User::getBalance, maxBalance)
            .list();
    // 3.处理vo
    return BeanUtil.copyToList(users, UserVO.class);
}
```
上面的的UserController由于注入了`IUserService`因此，而`UserServiceImpl`又实现了`ServiceImpl<UserMapper, User>` ，因此就具有了`lambdaQuery()`方法

lambdaQuery方法中除了可以构建条件之外，还需要在链式变成的最后添加一个list(),告诉mp我们需要的返回结果是一个list集合。还有可以是一下的选项：
* one(): 表示返回一个结果
* list(): 返回集合结果
* count(): 返回计数记过