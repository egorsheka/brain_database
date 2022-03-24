10.02.2022  19:55
Tags:  |
____

# MVC
maybe need to read https://www.baeldung.com/spring-web-contexts
https://www.sitepoint.com/rest-api/
https://stackify.com/spring-mvc/
https://mossgreen.github.io/Spring-Certification-Spring-MVC/#:~:text=META-INF%2Fresources-,Is%20the%20DispatcherServlet%20instantiated%20via%20an%20application%20context%3F,any%20application%20context%20is%20created

**Spring MVC Request Life Cycle**

1.  **Filter**: The filter applies to every request. There are several commonly used filters.
2.  **Dispatcher servlet**
3.  **Common services**: The common services will apply to every request to provide supports including i18n, theme, and file upload. Their configuration is defined in the DispatcherServlet’s WebApplicationContext.
4.  **Handler mapping**: This maps incoming requests to handlers (a method within a Spring MVC controller class). Spring MVC will automatically register a HandlerMapping implementation maps handlers based on HTTP paths expressed through the `@RequestMapping` annotation at the **type or method level** within controller classes.
5.  **Handler interceptor**: In Spring MVC, you can register interceptors for the handlers for implementing common checking or logic. For example, a handler interceptor can check to ensure that only the handlers can be invoked during office hours.
6.  **Handler exception resolver**: to deal with unexpected exceptions thrown during request processing by handlers.
7.  **View Resolver**: Spring MVC’s ViewResolver interface supports view resolution based on a logical name returned by the controller.
![[Pasted image 20220308214122.png]]
### DispatcherServlet
The DispatcherServlet delegates to special beans to process requests and render the appropriate responses.
A front controller is a common web application pattern where a single servlet delegates responsibility for a request to other components of an application to perform actual processing

____ 
### Links
- https://habr.com/ru/post/500572/