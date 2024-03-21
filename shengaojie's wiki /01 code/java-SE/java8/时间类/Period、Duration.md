
> [!what]
> 都表示一段时间  
> * Period：表示一段时间，天、月、年
> * Duration：表示一段时间，时分秒  
> 两者都实现了`TemporalAmount`



> [!how]  Period常用方法
```java
//获取两个LocalDate之间的时间  
LocalDate date = LocalDate.of(2024, 2, 20);  
LocalDate date1 = LocalDate.now();  
Period period = Period.between(date, date1);  
System.out.println("时间差为：" + period);

//of方法创建一个Period  
Period period = Period.ofMonths(2);  
//plusxxx方法在原先的period上增加一个时间段  
Period period1 = period.plusYears(2);  
  
//minus在原先的period上减去一个时间段  
Period period2 = period1.minus(Period.ofMonths(2));  
  
System.out.println("period is: " + period);  
System.out.println("period1 is: " + period1);  
System.out.println("period2 is: " + period2);  
  
//由一个TemporalAmount的实现类创建一个period  
Period period3 = Period.from(period);  
System.out.println("period3 is: " + period3);  
  
//通过parse方法，解析字符串为Period对象  
Period period4 = Period.parse("P2Y");  
System.out.println("period4 is: " + period4);  
  
//addTo方法，在原先的period上增加一个Temporal的实现类  
Temporal temporal = period.addTo(LocalDate.now());  
System.out.println("temporal is：" + temporal);  
  
//get方法获取period中的属性  
long month = period.get(ChronoUnit.MONTHS);  
System.out.println("month: " + month);  
  
  
System.out.println("period是否为负值：" + period.isNegative());  
System.out.println("period是否为0：" + period.isZero());

```


