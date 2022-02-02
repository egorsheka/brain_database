{{date:DD.MM.YYYY}}  {{time:HH:mm}}
Tags:  |
____

# Autowiring
## Autowiring modes


Mode | Explanation
-----| ----
`no` | (Default) No autowiring. Bean references must be defined by `ref` elements. Changing the default setting is not recommended for larger deployments, because specifying collaborators explicitly gives greater control and clarity. To some extent, it documents the structure of a system.
`byName` | Autowiring by property name. Spring looks for a bean with the same name as the property that needs to be autowired. For example, if a bean definition is set to autowire by name and it contains a `master` property (that is, it has a `setMaster(..)` method), Spring looks for a bean definition named `master` and uses it to set the property.
`byType` | Lets a property be autowired if exactly one bean of the property type exists in the container. If more than one exists, a fatal exception is thrown, which indicates that you may not use `byType` autowiring for that bean. If there are no matching beans, nothing happens (the property is not set).
`constructor` |Analogous to `byType` but applies to constructor arguments. If there is not exactly one bean of the constructor argument type in the container, a fatal error is raised.

https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-autowired-annotation

1.  Through a constructor
`constructor` = `byType`
```java
public class MovieRecommender 
{ 
	private final CustomerPreferenceDao customerPreferenceDao; 
	
	@Autowired public MovieRecommender(CustomerPreferenceDao customerPreferenceDao) 
	{ 
		this.customerPreferenceDao = customerPreferenceDao;
	}
}
```
As of Spring Framework 4.3, an `@Autowired` annotation on such a constructor is no longer necessary if the target bean defines only one constructor to begin with. However, if several constructors are available and there is no primary/default constructor, at least one of the constructors must be annotated with `@Autowired` in order to instruct the container which one to use. See the discussion on [constructor resolution](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-autowired-annotation-constructor-resolution) for details.

2.  Through setters or other methods
`byType` than `byName`
```java
public class School {  
  
    private Student student;  
  
 @Autowired  
 public void setStudent(Student student3) {  
        this.student = student3;  
 }  
}
```
3.  Through reflection, directly into fields
`byType` than `byName`
```java
public class School {  
  
    @Autowired  
 private Student student;  
 }
```

**Injection guidelines**

A general guideline, [which is recommended by Spring](http://docs.spring.io/spring/docs/4.2.x/spring-framework-reference/html/beans.html) (see the sections on [Constructor-based DI](https://docs.spring.io/spring/docs/4.2.x/spring-framework-reference/html/beans.html#beans-constructor-injection) or [Setter-based DI](https://docs.spring.io/spring/docs/4.2.x/spring-framework-reference/html/beans.html#beans-setter-injection)) is the following:

-   For mandatory dependencies or when aiming for immutability, use constructor injection
-   For optional or changeable dependencies, use setter injection
-   Avoid field injection in most cases




**Field injection drawbacks**

The reasons why field injection is frowned upon are as follows:

-   You cannot create immutable objects, as you can with constructor injection
-   Your classes have tight coupling with your DI container and cannot be used outside of it
-   Your classes cannot be instantiated (for example in unit tests) without reflection. You need the DI container to instantiate them, which makes your tests more like integration tests
-   Your real dependencies are hidden from the outside and are not reflected in your interface (either constructors or methods)
-   It is really easy to have like ten dependencies. If you were using constructor injection, you would have a constructor with ten arguments, which would signal that something is fishy. But you can add injected fields using field injection indefinitely. Having too many dependencies is a red flag that the class usually does more than one thing, and that it may violate the Single Responsibility Principle.
____ 
### Links
-