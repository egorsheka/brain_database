30.01.2022  20:54
Tags:  |
____

# Bean scopes

## singleton
Похож на паттерн GoF Singleton, создаётся при инициализации контекста.
Отличатеся от GoF Singleton тем, что его можно получить разные объекты (ссылки) класса, если бины были созданы с двух рахных контекстов. Разные контексты это разные объекты, а не разные метадаты.
```java
ApplicationContext apc = ClassPathXmlApplicationContext("bean.xml");
MySingletonClass msc = apc.getBean("mySingletonClass", MySingletonClass.class);
```
`getBean()` будет возвращать каждый раз одну и туже ссылку.
## prototype
```java
ApplicationContext apc = ClassPathXmlApplicationContext("bean.xml");
MyPrototypeClass mpc = apc.getBean("MyPrototypeClass", MyPrototypeClass.class);
```
`getBean()` будет возвращать каждый раз новую ссылку.
Если prototype бин является полем singleton бина, то 
1) DI выполнится один раз, singleton будет хранить одну и туже ссылку prototype 
2)  на каждый get будет новая ссылка (реализовано с помощью CGLIB)
```java
@Component  
@Scope(value = "prototype", proxyMode = ScopedProxyMode.TARGET_CLASS)  
public class MyPrototypeClass {  
}
```
3) Spring will create sub class (SGLIB proxy) for MySingletonClass. It will implement  override method the @Lookup method and return new bean
```java
@Component   
public class MySingletonClass { 
	
	@Lookup
	public MyPrototypeClass create(){
	return null;
	}
	/*Spring will create
	public MyPrototypeClass create(){
	return context.getBean("MyPrototypeClass", MyPrototypeClass.class);
	}
	*/
}
```
Такой метод можно сделать абстрактным, потому что его всё равно наследует прокси.
## prototype

____ 
### Links
-