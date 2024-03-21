
> [!why] 没有volatile会有什么样的问题？
> 从结果可以看出，`update`线程修改 `local`变量的值后，`reader`线程是看不见的（可见性）
```java
public class QuestionWithOutVolatile {  
	private final static int MAX = 10;  
	private static int local = 0;  
	  
	public static void main(String[] args) {  
		new Thread(() -> {  
			int value = local;  
			while(local < MAX){  
				//如果value 和 local的值不同的话，就打印一句话  
				if(value != local){  
					System.out.println("local的值已经被修改了，local is:" + local);  
					value = local;  
				}  
		  
			}  
		},"reader").start();  
		  
		  
		new Thread(() -> {  
			while(local < MAX){  
				//修改local的值  
				System.out.println(Thread.currentThread().getName() + "修改local的值：" + local++);  
				try {  
					//慢一点修改，防止线程1看不见  
					TimeUnit.SECONDS.sleep(2);  
				} catch (InterruptedException e) {  
					throw new RuntimeException(e);  
				}  
			}  
		  
		},"update").start();  
	}  
}
```

![[CleanShot 2023-12-20 at 21.17.04@2x.png]]


> [!notion] 为什么需要volatile
> `volatile`主要解决两个问题：
> 1. 保证不同线程之间对于共享变量操作时的 [[并发编程的特性#可见性|可见性]]。也就是说，如果有一个线程修改了 `volatile`修饰的变量的值，那么别的线程是可以看见的。
>	* 线程1读取到变量的值为0，并且存入到工作内存中去。此时线程2修改了该变量，会立即刷新到主存中，并且立即导致线程1工作内存中的变量的值失效。所以线程1必须要从主存中重新获取该值。
>	
> 2. 禁止对指令进行[[并发编程的特性#有序性|重新排序]]
> 	![[CleanShot 2023-12-20 at 20.39.45@2x.png|475]]
> 	只是禁止与 `volatile`修饰的指令进行重排序，该指令的前后指令不受影响。  
> 	如图中 `volatile`的作用：
> 	*  保证在执行到 `volatile int z = 20`的时候， `x = 0,y = 1`
> 	*  保证 `x++,y--`在`volatile int z = 20`之后执行  
> 	**至于 `x++,y--` 以及 `x = 0,y = 1`的顺序不能保证**


> [!NOTE] 使用
> `volatile`关键字只能用来修饰静态变量和实例变量，对于方法参数，局部变量以及类中常量（`static final修饰的`）都不能修饰


> [!important] 原理
> 被volatile修饰的变量，底层代码中会存在一个 `Lock`的前缀来修饰，其中的 `Lock`相当于是一个内存的屏障，该 `Lock`的作用如下：
> 1. 保证指令重排序时不会将后面的代码排到内存屏障之前
> 2. 保证指令重排序时不会将前面的代码排到内存屏障之后
> 3. 保证执行到内存屏障修饰的指令时，前面的代码都已经执行完成
> 4. 强制将线程工作内存中的值刷新到主存中
> 5. 如果是写操作会导致其他线程工作内存中的缓存数据失效


> [!example] volatile的使用场景
1. 利用可见性的特点，实现开关控制
```java
public class UseVolatile01 {  
	public static void main(String[] args) throws InterruptedException {  
		ThreadCloseable thread = new ThreadCloseable();  
		thread.start();  
		TimeUnit.SECONDS.sleep(1);  
		OtherThread otherThread = new OtherThread(thread);  
		otherThread.close();  
	}  
}  
  
class ThreadCloseable extends Thread{  
	private volatile boolean started = true;  
	  
	@Override  
	public void run() {  
	    // 另一个线程修改started的状态
		while(started){  
			//do something...  
		}  
	}  
	
	public void close(){  
		this.started =false;  
	}  
}  
	  
class OtherThread{  
	private ThreadCloseable threadCloseable;  
	  
	public OtherThread(ThreadCloseable threadCloseable) {  
		this.threadCloseable = threadCloseable;  
	}  
	  
	public void close(){  
		threadCloseable.close();  
	}  
}
```
2. 状态标记利用顺序特点
3. [[单例模式]]的double-check也是利用了顺序性特点


> [!compare] volatile VS [[synchronized]]
>1. `volatile`关键字是用来修饰实例变量和类变量的，`synchronized`是用来修饰方法或者是代码块的
>2. `volatile`无法保证原子性
>3. 对于可见性和有序性
>	* `synchronized`是通过排他的方式，使得代码串行化实现的。
>4. `volatile`不会使得线程阻塞，`synchronized`会让线程阻塞


