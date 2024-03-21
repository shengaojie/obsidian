
> [!question] MybatisPlus是如何获取实现CRUD的数据库表信息的？
> MyBatisPlus通过扫描实体类，并基于反射获取实体类信息作为数据库表信息。
> ![[CleanShot 2024-02-25 at 10.05.48@2x.png]]




> [!NOTE] @TableName：用来指定表名
>



> [!NOTE] @TableId：用来指定表中的主键字段信息
> * AUTO：数据库⾃增
> * INPUT：通过set⽅法⾃⾏输入
> * ASSIGN_ID：分配 ID，接⼝IdentifierGenerator的⽅法nextId来⽣成id，默认实现类为DefaultIdentifierGenerator雪花算法




> [!NOTE] @TableField：用来指定表中的普通字段信息
> 使用的场景：
> * 成员变量和数据库字段不一致
> * 成员变量是以is开头的boolean类型变量
> * 成员变量在数据库中不存在
> * 成员变量和数据库的关键字冲突

```java

@TableName("tb_user")
public class User {

@TableId(value="id",type=IdType.AUTO)
private Long id;

@TableField("username")
private String name;

@TableField("is_married")
private Boolean isMarried;

@TableField("`order`")
private Integer order;

@TableField(exist = false)
private String address; 

}

```
