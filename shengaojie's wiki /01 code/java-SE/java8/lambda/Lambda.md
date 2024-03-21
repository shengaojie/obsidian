
> [!why] 
> 行为参数化

![[CleanShot 2024-02-29 at 10.25.05@2x.png]]



> [!how]

1. 无参数，无返回值
```java
() -> {}
```

2. 带有一个参数时
```java
Consumer<String> fun = (args) -> {  
	System.out.println(args);  
};

//只有一个参数时，小括号可以省略
Consumer<String> fun = args -> {  
	System.out.println(args);  
};

```

3. 方法体中只有一条语句时
	* 可以省略{}
	* 如果需要return，return也可以省略
```java
Thread thread = new Thread(() ->  
	System.out.println("hello")  
);


(String s) -> s.length()  //表示返回s的长度
() -> 42  //无参数，返回42

```



> [!fire] 哪些地方可以使用Lambda

* 在[[函数式接口]]上可以使用，Lambda表达式允许你直接以内联的形式为函数式接口的抽象方法提供实现，并将整个表达式作为函数式接口的实例。
* 我们需要保证的是：Lambda表达式的签名要和函数式接口的抽象方法保持一致
* 函数式接口会使用`@FunctionalInterface`来修饰


