
> [!what] 
> 对于一些比较重要的数据，我们往往会采用逻辑删除的方案，即：
> - 在表中添加一个字段标记数据是否被删除
> -  当删除数据时把标记置为true
> - 查询时过滤掉标记为true的数据

原先的删除语句是delete语句，逻辑删除实际上是update语句
```sql
update address set deleted= 1 where id = ? and deleted = 0
```

一旦采用了逻辑删除，所有的查询和删除逻辑都要跟着变化，非常麻烦。为了解决这个问题，MybatisPlus就添加了对逻辑删除的支持。

> [!attention]
> **注意**，只有MybatisPlus生成的SQL语句才支持自动的逻辑删除，自定义SQL需要自己手动处理逻辑删除。



> [!how] 

1. 给`address`表添加一个逻辑删除字段：
```sql
alter table address add deleted bit default b'0' null comment '逻辑删除';
```

2. 给`address`实体类增加一个`deleted`字段
```java
# 逻辑删除字段
private Boolean deleted;
```


3. 在`application.yaml`中配置逻辑删除字段
```yaml
mybatis-plus:
  global-config:
    db-config:
      logic-delete-field: deleted # 全局逻辑删除的实体字段名(since 3.3.0,配置后可以忽略不配置步骤2)
      logic-delete-value: 1 # 逻辑已删除值(默认为 1)
      logic-not-delete-value: 0 # 逻辑未删除值(默认为 0)

```



> [!problem] 逻辑删除存在的问题
> **注意**： 逻辑删除本身也有自己的问题，比如：
> - 会导致数据库表垃圾数据越来越多，从而影响查询效率
> - SQL中全都需要对逻辑删除字段做判断，影响查询效率  
> 因此可以采用把数据迁移到其它表的办法。



