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
`byType` than `byName`
```java
public class School {  
  
    @Autowired  
 private Student student;  
 }
```
____ 
### Links
-