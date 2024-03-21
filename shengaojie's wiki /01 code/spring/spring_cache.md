
> [!what] 
> * Spring Cache 是一个框架，实现了基于注解的缓存功能，只需要简单地加一个注解，就能实现缓存功能。
> * Spring Cache 提供了一层抽象，底层可以切换不同的缓存实现，例如：
> 	* EHCache
> 	- Caffeine
> 	- Redis(常用)
> 



> [!how] 

1. 导入Spring Cache的依赖
```xml
<dependency>  
	<groupId>org.springframework.boot</groupId>  
	<artifactId>spring-boot-starter-cache</artifactId>  
</dependency>  
```
2. 导入具体使用缓存的依赖，这里是redis
```xml
<dependency>  
	<groupId>org.springframework.boot</groupId>  
	<artifactId>spring-boot-starter-data-redis</artifactId>  
</dependency>
```
3. 在启动类上加上注解`@EnableCaching`,表示开启注解缓存功能



> [!para] 具体的注解
> 

> [!NOTE]  @CachePut
> 作用：将方法的返回值放到缓存中    
> * value(cacheNames): 缓存的名称, 每个缓存名称下面可以有很多key  
> * key: 缓存的key ----------> 支持Spring的表达式语言SPEL语法  
> **下面在缓存中对应的key为：userInfo::2**

```java
@PostMapping  
@CachePut(cacheNames = "userInfo",key = "#user.id")  
public User save(@RequestBody User user){  
	userMapper.insert(user);  
	return user;  
}
```



> [!NOTE] @Cacheable
> 1. 在方法执行之前，先查询缓存中有没有数据，如果有则直接返回数据
> 2. 如果缓存中没有，则调用所修饰的方法，最后将方法的返回数据存入缓存中

```java
@GetMapping  
@Cacheable(cacheNames = "userInfo",key = "#id")  
public User getById(Long id){  
	User user = userMapper.getById(id);  
	return user;  
}
```


> [!NOTE] CacheEvict
> 删除缓存中的一条或者是多条数据  
> * allEntries：表示删除所有的userInfo::的缓存
> 

```java
@DeleteMapping  
@CacheEvict(cacheNames = "userInfo",key = "#id")  
public void deleteById(Long id){  
	userMapper.deleteById(id);  
}
```

```java
@DeleteMapping("/delAll")  
@CacheEvict(cacheNames = "userInfo",allEntries = true)   
public void deleteAll(){  
	userMapper.deleteAll();  
}
```