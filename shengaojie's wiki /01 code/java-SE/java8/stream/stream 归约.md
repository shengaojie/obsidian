
> [!what] 
> 将流中的元素组合起来，得到一个值。进行更加复杂的查询操作

![[CleanShot 2024-03-01 at 14.03.43@2x.png]]

> [!how] 
1. reduce()：有初始值的版本
```java
int product = numbers.stream().reduce(1, (a, b) -> a * b); 
```
参数1：初始值
参数2：一个BinaryOperator\<T>将两个元素结合起来产生新的值

2. reduce(): 无初始值的版本
```java
Optional<Integer> sum = numbers.stream().reduce((a, b) -> (a + b)); 
```

因为没有初始值，所以返回一个Optional\<Integer>




> [!NOTE] 使用reduce来求最大最小值

```java
Optional<Integer> max = numbers.stream().reduce(Integer::max); 
```

