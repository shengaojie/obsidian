![[CleanShot 2024-03-01 at 09.42.38@2x.png]]
> [!中间操作] 

1. 什么是中间操作？
中间操作是为了形成一条流的流水线，类似于[[建造者模式]]，用调用链的方式进行一系列的转换。


2. 有哪些中间操作
* list  filter 
作用：筛选我们需要的元素
参数类型：Predicate\<T>

```java
List<Dish> vegetarianMenu = menu.stream() 
								.filter(Dish::isVegetarian) 
                                .collect(toList()); 
```



* list limit 
作用：限制流中返回元素的个数
参数类型：需要一个long类型
```java
List<Dish> dishes = menu.stream() 
                        .filter(d -> d.getCalories() > 300) 
                        .limit(3) 
                        .collect(toList()); 
```
* list  sorted
作用：给流中的元素排序
参数类型：Comparator\<T> 



* list distinct
作用：筛选出各异的元素
参数类型：无参数
```java
List<Integer> numbers = Arrays.asList(1, 2, 1, 3, 3, 2, 4); 
numbers.stream()  
       .filter(i -> i % 2 == 0) 
	   .distinct() 
       .forEach(System.out::println); 
```



* list skip
作用：跳过前面的n个元素，如果不足n个则返回一个空的流
参数：long
```java
List<Dish> dishes = menu.stream() 
                        .filter(d -> d.getCalories() > 300) 
                        .skip(2) 
                        .collect(toList()); 
```
* list  [[stream的映射]]





> [!终端操作]

1. 什么是终端操作？
根据中间操作的流水线，生成最后的结果，类似于[[建造者模式]]中的builder方法

2. 常见的终端操作
* list forEach：对流中的每一个元素应用Lambda，接受一个Consumer接口


* list  count: 返回流中元素的个数。这一操作返回 long 


* list  collect: 把流归约成一个集合