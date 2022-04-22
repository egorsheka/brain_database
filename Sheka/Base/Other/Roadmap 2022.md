08.01.2021  14:22
Tags:  |
____

# Roadmap 2022
#### English
evry day:
- one text to translate 
- learn words from preveis texts and lessons
- 3 page from book

#### Spring :
- core:
	- Inversion of Control `done`
	- Autowiring `done`
	- Bean life cycle
	- Bean scopes 
	- Annotation and Java config
	- AplicationContext and BeanFactory
	- Profiles
	- Validation
	- AOP
- mvc
- security
- Data
- integration
- testing
#### Git
#### Hibernate
#### HTTP
#### Java 
- object 
- exception
- generic 
- multithreading
- functional and stream
- string
- java API
- collections
- servlet







### Need to read later
прочитать про BPP https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-extension-bpp
закончить Bean Scopes
https://spring.io/blog/2004/08/06/method-injection/
https://www.youtube.com/watch?v=muJOdyoE7Gk
также понять разеицу cglib vs jdk poxy

In contrast to the other scopes, Spring does not manage the complete lifecycle of a prototype bean. The container instantiates, configures, and otherwise assembles a prototype object and hands it to the client, with no further record of that prototype instance. Thus, although initialization lifecycle callback methods are called on all objects regardless of scope, in the case of prototypes, configured destruction lifecycle callbacks are not called. The client code must clean up prototype-scoped objects and release expensive resources that the prototype beans hold. To get the Spring container to release resources held by prototype-scoped beans, try using a custom [bean post-processor](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-extension-bpp), which holds a reference to beans that need to be cleaned up.

https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-other-injection
https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-custom
____ 
### Links
- [[_Brain]]