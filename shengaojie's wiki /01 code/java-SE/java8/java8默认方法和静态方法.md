
> [!what] 什么是默认方法
> Java 8中允许接口中包含具有具体实现的方法，该方法称为“默认方法”，默认方法使用 default 关键字修饰。

```java
interface MyFunc<T>{
	T fucn(int a);

	default String getName(){
		return "hello default method";
	}
}
```


> [!NOTE] 默认方法处理冲突的原则

1. 类中的方法优先级最高。类或父类中声明的方法的优先级高于任何声明为默认方法的优先级。  
2. 如果无法依据第一条进行判断，那么子接口的优先级更高：函数签名相同时，优先选择拥有最具体实现的默认方法的接口，即如果B继承了A，那么B就比A更加具体。  
```java
interface B extends A{  
	@Override  
	default void hello(){  
		System.out.println("hello from B");  
	}  
}  
  
class C implements B, A {  
  
	public void test(){  
		hello();  //这里打印的是hello from B 因为B比A更加的具体
	}  
}
```

3. 最后，如果还是无法判断，继承了多个接口的类必须通过显式覆盖和调用期望的方法，

```java
class C1 implements B1, A1{  
  
	//因为此时B1和A1一样的具体，需要显示的指定调用哪一个接口中的hello方法  
	// xxx.super.method()  
	@Override  
	public void hello() {  
		A1.super.hello();  
	}  
}
```



> [!NOTE] 静态方法

```java
interface MyFunc<T>{
	T fucn(int a);

	default String getName(){
		return "hello default method";
	}
	static void show(){
		 System.out.println("hello default method");
	}
}
```
