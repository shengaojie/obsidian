
> [!why] 
> 

在数据库user表中有一个字段`info`，是JSON类型 ，数据格式为
```json
{"age": 20, "intro": "佛系青年", "gender": "male"}
```
![[CleanShot 2024-02-26 at 15.24.07@2x.png]]

但是目前对应的实体类User中的info字段为String类型。
* 这样会有一个很大的问题，就是想要获取String类型中对应的属性不方便；
* 但是如果将info字段转换为对象类型的话，在导入数据库的时候又需要转为String，读取的时候又要从String转为对象，也很麻烦。

`mybatisplus`为了解决这个问题，提供了很多特殊类型的处理器，JSON就可以使用`JacksonTypeHandler`处理器。



> [!how] 

1. 定义一个实体和数据库中的info字段的属性匹配
```java
@Data 
public class UserInfo { 
	private Integer age; 
	private String intro; 
	private String gender;
}
```


2. 使用类型处理器
修改User类的info字段的类型为UserInfo,并且声明类型处理器
![[CleanShot 2024-02-26 at 15.37.09@2x.png]]