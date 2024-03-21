
> [!notion] 
> 通过@ + 注解名称的方式出现，用于修饰解释 包、类、方法、属性、构造器、局部变量等数据信息



> [!NOTE] 注解的本质
> * 注解的本质是一个接口
> *  使用注解的地方相当于是new了一个接口的实现类

![[CleanShot 2024-01-29 at 21.39.52@2x.png]]


> [!NOTE] 常见的元注解
> * 所谓的元注解，就是修饰注解的注解
> * `@Target(ElementType.xxx)`:表示一个注解可以作用在哪些地方，如方法上，类上，成员变量上等
> * @Retention(RetentionPolicy.xxx):表示注解的作用范围，主要下面三种：
> 	* SOURCE: 编译器使用后，直接丢弃这种策略的注释
> 	* CLASS: 编译器将把注解记录在 class 文件中. 当运行 Java 程序时, JVM 不会保留注解。 **这是默认**
> 	* RUNTIME:编译器将把注解记录在 class 文件中. 当运行 Java 程序时, JVM 会保留注解. **程序可以通过反射获取该注解**



> [!NOTE] 可以通过[[reflection]]获取注解中的值
> 其中的MyTest是一个自定义的注解，并且有aaa，bbb，ccc三个属性值，并且将该注解作用到了一个`AnnotationTest`的类上
> * `isAnnotationPresent(xxx.class)`:判断是否有使用xxx注解
> * `getDeclaredAnnotation(xxx.class)`:获取特定的xxx注解
```java
public void test() throws NoSuchMethodException {  
	Class<AnnotationTest> cls = AnnotationTest.class;  
	if (cls.isAnnotationPresent(MyTest.class)) {  
		MyTest myTest = (MyTest) cls.getDeclaredAnnotation(MyTest.class);  
		System.out.println("aaa: " + myTest.aaa());  
		System.out.println("bbb: " + myTest.bbb());  
		System.out.println("ccc: " + myTest.ccc());  
	}  
	  
	System.out.println("hello world");  
}
```
