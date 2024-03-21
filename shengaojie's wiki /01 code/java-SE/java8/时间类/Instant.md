
> [!what] 
> 时间戳




> [!how] instant的常见用法
> 
```java
Instant now = Instant.now();  
System.out.println("当前的时间戳为：" + now);  
  
//表示从1970年开始往后加3s  
Instant instant = Instant.ofEpochSecond(3);  
System.out.println(instant);  
  
//表示从1970年开始往后加3s + 1_000_000_000ns,也就是4s  
Instant instant1 = Instant.ofEpochSecond(3, 1_000_000_000);  
System.out.println(instant1);  
  
//表示从1970年开始往后加(3s - 100_000_000ns)  
Instant instant2 = Instant.ofEpochSecond(3, -100_000_000);  
System.out.println(instant2);  
  
//会报错UnsupportedTemporalTypeException  
// int dayofWeek = now.get(ChronoField.DAY_OF_WEEK);
```