
> [!what] 
> 1. 作为`mybatis`**单表查询的增强版**
> 2. 通过`Wrapper`来代替复杂的`<where></where>标签`



> [!how] 
1. 引入MybatisPlus的起步依赖
MyBatisPlus官方提供了starter，其中集成了Mybatis和MybatisPlus的所有功能，并且实现了自动装配效果。**因此我们可以用MybatisPlus的starter代替Mybatis的starter：**
```xml
<!--MybatisPlus--> 
<dependency>
	<groupId>com.baomidou</groupId> 
	<artifactId>mybatis-plus-boot-starter</artifactId> 
	<version>3.5.3.1</version> 
</dependency>
```

2. 定义Mapper
自定义的Mapper继承MybatisPlus提供的`BaseMapper接口`：
![[CleanShot 2024-02-25 at 10.02.48@2x.png]]
其中的`BaseMapper<>`要注明泛型

