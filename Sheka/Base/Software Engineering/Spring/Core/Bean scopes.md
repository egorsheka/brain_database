30.01.2022  20:54
Tags:  |
____

# Bean scopes

## singleton
Похож на паттерн GoF Singleton, создаётся при инициализации контекста.
Отличатеся от GoF Singleton тем, что его можно получить разные объекты (ссылки) класса, если бины были созданы с двух рахных контекстов.
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
2)  на каждый get будет новая ссылка (реализовано с помощью CGlib)
```java
@Component  
@Scope(value = "prototype", proxyMode = ScopedProxyMode.TARGET_CLASS)  
public class MyPrototypeClass {  
}
```
3) 
## prototype

____ 
### Links
-