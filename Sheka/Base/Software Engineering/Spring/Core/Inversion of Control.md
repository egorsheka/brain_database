02.02.2022  15:24
Tags:  |
____

# Inversion of Control
This chapter covers the Spring Framework implementation of the Inversion of Control (IoC) principle. IoC is also known as dependency injection (DI). It is a process whereby objects define their dependencies (that is, the other objects they work with) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The container then injects those dependencies when it creates the bean. 

DI exists in two major variants: [Constructor-based dependency injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-constructor-injection) and [Setter-based dependency injection](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-setter-injection).

The `org.springframework.context.ApplicationContext` interface represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the beans by reading configuration metadata. The configuration metadata is represented in XML, Java annotations, or Java code.

```java
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
```

#### Dependency Injection

Can be:

-   Field injection
-   Constructor injection
-   Method injection
Setter-based DI is accomplished by the container calling setter methods on your beans after invoking a no-argument constructor or a no-argument `static` factory method to instantiate your bean.
-   Interface injection
```java
public class CommandManager implements ApplicationContextAware { 
	
	private ApplicationContext applicationContext; 
	
	public Object process(Map commandState) { 
		Command instance command.setState(commandState);
		return command.execute(); 
	} 
	
	protected Command createCommand() { 
	 this.applicationContext.getBean("command", Command.class); 
	} 
		
	public void setApplicationContext( ApplicationContext applicationContext)
		throws BeansException { 
		this.applicationContext = applicationContext; 
	} 
}
```

____ 
### Links
-