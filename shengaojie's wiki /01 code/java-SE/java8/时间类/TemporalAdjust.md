
> [!what] 
> 为了更加灵活的操作时间，可以将一个`Temporal`转换成另一个`Temporal`

```java
@Test  
public void test04(){  
	// 请设计一个NextWorkingDay类，该类实现了TemporalAdjuster接口，能够计算明天  
	// 的日期，同时过滤掉周六和周日这些节假日  
	LocalDate date = LocalDate.of(2023, 11, 18);  
	LocalDate date1 = date.with(new TemporalAdjuster() {  
	@Override  
	public Temporal adjustInto(Temporal temporal) {  
		//temporal.get(ChronoField.DAY_OF_WEEK) 返回的是一个int类型  
		//需要通过DayOfWeek来返回一个具体的星期几  
		DayOfWeek dayOfWeek = DayOfWeek.of(temporal.get(ChronoField.DAY_OF_WEEK));  
		int addDay = 1;  
		if (dayOfWeek == DayOfWeek.FRIDAY) {  
			addDay = 3;    
		} else if (dayOfWeek == DayOfWeek.SATURDAY) {  
			addDay = 2;  
		}    
		return temporal.plus(addDay, ChronoUnit.DAYS);  
		}  
	});  
	  
	System.out.println(date1);  
	  
	  
	//推荐使用TemporalAdjusters类中的ofDateAdjuster方法创建对象  
	//上面的代码改写为  
	LocalDate date2 = date.with(TemporalAdjusters.ofDateAdjuster(temporal -> {  
	//temporal.get(ChronoField.DAY_OF_WEEK) 返回的是一个int类型  
	//需要通过DayOfWeek来返回一个具体的星期几  
	DayOfWeek dayOfWeek = DayOfWeek.of(temporal.get(ChronoField.DAY_OF_WEEK));  
	int addDay = 1;  
	if (dayOfWeek == DayOfWeek.FRIDAY) {  
		addDay = 3;  
	  
	} else if (dayOfWeek == DayOfWeek.SATURDAY) {  
		addDay = 2;  
	}  
	  
	return temporal.plus(addDay, ChronoUnit.DAYS);  
	}));  
	  
	System.out.println(date2);    
}
```