
> [!map] 
> 

* 作用：接受一个函数，将这个函数应用到流中的每一个元素中，生成一个新的元素，生成的还是流。
* 参数：function<\T,R>
```java
List<String> dishNames = menu.stream() 
                             .map(Dish::getName) 
                             .collect(toList()); 
```



> [!why] 为什么需要flapMap
> flatmap方法让你把一个流中的每个值都换成另一个流，然后把所有的流连接
起来成为一个流。 

![[CleanShot 2024-03-01 at 10.00.06@2x.png]]


```java
List<String> uniqueCharacters =  words.stream() 
			 .map(w -> w.split("")) 
			 .flatMap(Arrays::stream)  
			 .distinct() 
			 .collect(Collectors.toList());
```