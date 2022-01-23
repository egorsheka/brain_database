22.12.2020  18:25
Tags: 
____

# Spring
## Based on DI(IoC) conversion


- Inversion of Control, IoC — Архитектурное решение, при котором поток управления программы контролируется фреймворком.

В обычной программе программист сам решает, в какой последовательности делать вызовы процедур. Но если используется фреймворк, программист может разместить свой код в определенных точках выполнения (используя callback или другие механизмы), затем запустить «главную функцию» фреймворка, которая обеспечит все выполнение и вызовет код программиста тогда, когда это будет необходимо. Как следствие, происходит утеря контроля над выполнением кода — это и называется инверсией управления (фреймворк управляет кодом программиста, а не программист управляет фреймворком).

Dependency injection. Внедрение зависимостей — это стиль настройки объекта, при котором поля объекта задаются внешней сущностью

Спринг может:
управляет бинами(Managed beans are created, destroyed and wired)
Конфигурирует их с помощью XML or Groovy files(bean definitions), annotations or Java/Kotlin-based configuration 
Связывает бины благодоря dependency lookup or dependency injection





The `org.springframework.context.ApplicationContext` interface represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the beans by reading configuration metadata. The configuration metadata is represented in XML, Java annotations, or Java code.
```java
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
```

####  Dependency Injection
Dependency injection part of IoC (DI) is a process whereby objects define their dependencies (that is, the other objects with which they work) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method.

Can be:
- Field injection
- Constructor injection 
- Method injection
- Interface injection

Setter-based DI is accomplished by the container calling setter methods on your beans after invoking a no-argument constructor or a no-argument `static` factory method to instantiate your bean.


____ 
### Links
- [[_Brain]]