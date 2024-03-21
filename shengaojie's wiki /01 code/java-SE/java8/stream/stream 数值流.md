
> [!why] 
> 为了减少拆箱的成本

下面的代码需要每次拆箱成一个int类型，在进行求和。并没有提供现成的sum方法
```java
int calories = menu.stream() 
                   .map(Dish::getCalories) 
                   .reduce(0, Integer::sum); 
```


> [!NOTE] 解决问题的方法： 
引入了三个原始类型特化流接口，`IntStream`、`DoubleStream和`
`LongStream`，分别将流中的元素特化为int、long和double，从而避免了暗含的装箱成本。并且提供了如sum、max等方法


> [!NOTE] 映射到数值流
```java
int calories = menu.stream() 
				   .mapToInt(Dish::getCalories)  
				   .sum(); 
```



> [!NOTE] 转回对象流
> 
```java
IntStream intStream = menu.stream().mapToInt(Dish::getCalories); 
//将数值流转为对象流
String<Integer> stream = intStream.boxed();
```




> [!NOTE] 默认值OptionalInt

如果计算IntStream中的最大的元素，如何区分流中的最大元素是0还是流中没有元素存在呢？
使用[[Optional]]的原始类型特化版本:OptionalInt、OptionalDouble和OptionalLong

```java
OptionalInt maxCalories = menu.stream() 
                              .mapToInt(Dish::getCalories) 
                              .max(); 
//如果没有最大值的话，可以设置一个默认值
int max = maxCalories.orElse(1);
```


