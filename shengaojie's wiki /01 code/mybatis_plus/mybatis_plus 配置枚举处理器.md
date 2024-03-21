
> [!what] 
> 我们在表示对象某一个状态的时候通常使用`private Integer status;`这样的表示形式，但是如果状态多的话，这样并不是很直观。因此需要将Integer类型转换为枚举类型，但是数据库中的对应的字段依然是int类型，如何**将这里的枚举类型和数据库中的int类型做自动转换**，就需要配置枚举处理器。
 


> [!how] 

1. 告诉`mybatisplus`枚举中的哪个字段的值作为数据库值,使用`@EnumValue`注解来标记属性
```java
@Getter  
public enum UserStatus {  
	NORMAL(1, "正常"),  
	FROZEN(2, "冻结");  
	  
	@EnumValue  
	private final int value;  
	@JsonValue  
	private final String desc;  
	  
	UserStatus(int value, String desc) {  
		this.value = value;  
		this.desc = desc;  
	}  
}
```


> [!@JsonValue] 
> 注解标记JSON序列化时展示的字段

如果没有该注解的话，前端页面的展示该枚举为
![[CleanShot 2024-02-26 at 15.13.18@2x.png]]
加上该注解在该枚举类型的desc上之后：
![[CleanShot 2024-02-26 at 15.18.45@2x.png]]

2. 配置枚举处理器
在`application.yaml`文件中添加配置

```YAML
mybatis-plus:
  configuration:
    default-enum-type-handler: com.baomidou.mybatisplus.core.handlers.MybatisEnumTypeHandler
```

