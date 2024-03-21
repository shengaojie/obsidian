
> [!what] 
> 一种更加高级的归约的方式，更能体现函数式编程而不是指令时编程。
> 通过传递给collect()方法一个`Collector`的实现，来给流中的元素做汇总的操作。




> [!预定义收集器] 
> 在Collectors类中已经提供了一些现有的收集器，主要有三大功能，分别是汇总数据，元素分区，元素分组


> [!NOTE] 汇总值

* list 查找最大最小值
```java
Comparator<Dish> dishCaloriesComparator = 
    Comparator.comparingInt(Dish::getCalories); 

Optional<Dish> mostCalorieDish = menu.stream() 
						        .collect(maxBy(dishCaloriesComparator)); 
```



* list 获取总和、平均值

```java
int totalCalories = menu.stream().collect(summingInt(Dish::getCalories)); 
double avgCalories = 
    menu.stream().collect(averagingInt(Dish::getCalories)); 
```



* list IntSummaryStatistics类
包含着数量、总和、最小值、最大值、平均数信息
```java
IntSummaryStatistics menuStatistics = 
        menu.stream().collect(summarizingInt(Dish::getCalories)); 

//IntSummaryStatistics{count=9, sum=4300, min=120, average=477.777778, max=800} 
```



* list 连接字符串joining
通过，分割，打印所有的菜品的名字
```java
String shortMenu = menu.stream().map(Dish::getName).collect(joining(", ")); 
```


> [!NOTE] 元素分组
> 通过给groupingBy方法传递了一个Function作为分类函数

下面的例子将小于400划分成一个组，400~700划分成一个组，其余的成一个组
```java
Map<CaloricLevel, List<Dish>> dishesByCaloricLevel = menu.stream().collect(         groupingBy(dish -> { 
               if (dish.getCalories() <= 400) return CaloricLevel.DIET;                else if (dish.getCalories() <= 700) return 
    CaloricLevel.NORMAL; 
        else return CaloricLevel.FAT; 
         } )); 

```

* list 多级分组
其中的groupingBy函数，可以接受第二个收集器
```java
Map<Dish.Type, Map<CaloricLevel, List<Dish>>> dishesByTypeCaloricLevel = 
menu.stream().collect( 
      groupingBy(Dish::getType,  
         groupingBy(dish -> {  
            if (dish.getCalories() <= 400) return CaloricLevel.DIET;                 else if (dish.getCalories() <= 700) return CaloricLevel.NORMAL; 
	     else return CaloricLevel.FAT; 
          } ) 
      ) 
); 

//{MEAT={DIET=[chicken], NORMAL=[beef], FAT=[pork]},  
//  FISH={DIET=[prawns], NORMAL=[salmon]}, 
//  OTHER={DIET=[rice, seasonal fruit], NORMAL=[french fries, pizza]}} 
```

![[CleanShot 2024-03-01 at 14.21.45@2x.png]]

* list 把收集器中的结果转换为另外一个类型
```java
Map<Dish.Type, Dish> mostCaloricByType = 
	    menu.stream() 
	        .collect(groupingBy(Dish::getType, 
	                 collectingAndThen( 
	                     maxBy(comparingInt(Dish::getCalories)),  
	                 Optional::get)));  
```
![[CleanShot 2024-03-01 at 14.44.20@2x.png]]



> [!NOTE] 元素分区
> 分区是分组的特殊情况：由一个谓词（返回一个布尔值的函数）作为分类函数

```java
Map<Boolean, List<Dish>> partitionedMenu = 
             menu.stream().collect(partitioningBy(Dish::isVegetarian));  
```

和分组一样其中的partitioningBy的第二个参数可以在接受一个收集器。

```java
Map<Boolean, Map<Dish.Type, List<Dish>>> vegetarianDishesByType = 
menu.stream().collect( 
        partitioningBy(Dish::isVegetarian,  
                       groupingBy(Dish::getType))); 

// 结果为:{false={FISH=[prawns, salmon], MEAT=[pork, beef, chicken]}, 
```