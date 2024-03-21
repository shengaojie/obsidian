
> [!构建流的方式] 

1. 由值创建流
```java
Stream<String> stream = Stream.of("Java 8 ", "Lambdas ", "In ", "Action"); 
```


2. 由数组创建流
```java
int[] numbers = {2, 3, 5, 7, 11, 13}; 
int sum = Arrays.stream(numbers).sum(); 
```

3. 无限流
* 使用iterate方法
```java
Stream.iterate(0, n -> n + 2) 
      .limit(10) 
      .forEach(System.out::println); 
```
生成一个从0开始不断加2的数字，一个生成10个。其中的iterate方法接受一个UnaryOperator\<T>类型的接口

* 使用generate生成
```java
Stream.generate(Math::random) 
      .limit(5) 
      .forEach(System.out::println); 
```
generate接受一个Supplier\<T>类型的接口



> [!attention] 
> 在使用无限流的时候，需要使用limit方法来限制它的大小，否则无法使用排序、归约和终端操作

4. 生成一个范围内的数值，使用[[stream 数值流]
```java
//生成1~100之间的偶数
IntStream evenNumbers = IntStream.rangeClosed(1, 100)  
                                 .filter(n -> n % 2 == 0);
```