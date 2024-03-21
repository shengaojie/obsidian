
> [!what] 时间类的相关api
> 其中的`LocalDateTime`


> [!paragraph] 三者之间的转换
> 

1. 通过`LocalDate`和`LocalTime`构造`LocalDateTime`
```java
//a.通过LocalDateTime.of方法
LocalTime time = LocalTime.now();  
LocalDate date = LocalDate.now();  
LocalDateTime ldt2 = LocalDateTime.of(date, time);


//b.LocalTime的atDate方法和LocalDate的atTime方法
LocalDateTime ldt4 = time.atDate(date);  
LocalDateTime ldt5 = date.atTime(time);
```

2. 将`LocalDateTime`转换为`LocalDate`或者是`LocalTime`
```java
LocalDateTime localDateTime = LocalDateTime.now();  
LocalDate localDate = localDateTime.toLocalDate();  
LocalTime localTime = localDateTime.toLocalTime();
```



> [!NOTE] 时间的修改

1. 直接修改
```java
LocalDateTime now = LocalDateTime.now();  
System.out.println("now is: " + now);  
//操作,以直观的方式直接修改  
LocalDateTime dateTime = now.withHour(9)  
							.withMinute(9)  
							.withSecond(9)  
							.with(ChronoField.DAY_OF_MONTH,10);  
System.out.println("dateTime is: " + dateTime);
```


2. 相对方式修改
```java
LocalDateTime dateTime2 = now.plusDays(2)  
								.plusHours(2)  
								.plusYears(2);  
System.out.println("dateTime2 is: " + dateTime2);
```

> [!NOTE] 两个时间点之间的时间
> 
```java
LocalTime localTime = LocalTime.of(3, 3, 3);  
LocalTime localTime1 = LocalTime.of(3, 3, 5);  
System.out.println(ChronoUnit.SECONDS.between(localTime,localTime));
```


> [!NOTE] 字符串格式转时间格式
```java
//解析2024-02-10T09:09:09.982726  
LocalDateTime dateTime1 = LocalDateTime.parse("2024-02-10T09:09:09.982726",DateTimeFormatter.ISO_DATE_TIME);  
```



> [!NOTE] 时间格式转字符串格式
> 
```java
//格式化为字符串格式  
String format = dateTime1.format(DateTimeFormatter.ISO_LOCAL_DATE);
```
