25.01.2022  13:16
Tags:  |
____

# Bean life cycle

#### 1. Парсирование конфигурации и создание BeanDefinition

1.  Xml конфигурация — ClassPathXmlApplicationContext(“context.xml”)
2.  Конфигурация через аннотации с указанием пакета для сканирования — AnnotationConfigApplicationContext(“package.name”)
3.  Конфигурация через аннотации с указанием класса (или массива классов) помеченного аннотацией @Configuration -AnnotationConfigApplicationContext(JavaConfig.class). Этот способ конфигурации называется — JavaConfig.
4.  Groovy конфигурация — GenericGroovyApplicationContext(“context.groovy”)

**XmlBeanDefinitionReader** или **AnnotatedBeanDefinitionReader** считывает из XML все декларации бинов, сканирует XML и все что мы там пишем переводит в **BeanDefinitions** — это объекты, которые хранят информацию про бины. Каждый **BeanDefinition** помещается в Map и хранится в классе **DefaultListableBeanFactory**.

```java
Map<String, BeanDefinition> beanDefinitionMap = new ConcurrentHashMap<String, BeanDefinition>(64);
```

#### 2. Настройка созданных BeanDefinition



отрабатывает **BeanFactoryPostProcessor**.

Это интерфейс, который позволяет настраивать **BeanDefinitions** до того, как создаются бины. Он работает на этапе, когда кроме **BeanDefinitions** еще ничего нету (когда никаких бинов еще нет, ничего нет) и может что-то “подкрутить” в **BeanDefinitions**.

#### 4. Создание экземпляров бинов 
Созданием экземпляров бинов занимается _BeanFactory_ при этом, если нужно, делегирует это кастомным _FactoryBean_.
![[Pasted image 20220126155402.png]]

####  кастомный FactoryBean
```java
public class ColorFactory implements FactoryBean<Color> 
{ 
	@Override public Color getObject() throws Exception 
	{ 
		Random random = new Random(); 
		Color color = new Color(random.nextInt(255), random.nextInt(255), random.nextInt(255));
		return color; 
	}
	@Override public Class<?> getObjectType() { return Color.class; } 
	
	@Override public boolean isSingleton() { return false; } 
}
```

```json
<?xml version="1.0" encoding="UTF-8"?> 
<beans ...> 
	<bean id="colorFactory" class="com.malahov.temp.ColorFactory"></bean> 
</beans>
```

Теперь создание бина типа _Color.class_ будет делегироваться ColorFactory, у которого при каждом создании нового бина будет вызываться метод **getObject**.  

Для тех кто пользуется JavaConfig, этот интерфейс будет абсолютно бесполезен.
  
  #### 4. Интерфейсы  `ApplicationContextAware` and `BeanNameAware`
  Вызываются переопределённые сеттеры данных интерфейсов и инджектят `ApplicationContext`
  https://russianblogs.com/article/846831964/
  
In general, you should avoid it, because it couples the code to Spring and does not follow the Inversion of Control style, where collaborators are provided to beans as properties.

#### 5. Настройка созданных бинов

**BeanPostProcessor** — это интерфейс. Он позволяет настраивать бины прежде чем они попадут в контейнер.
1. **_postProcessBeforeInitialization()_** — вызывается до init() метода.  

2. init() методы:
Multiple lifecycle mechanisms configured for the same bean, with different initialization methods, are called as follows:
- Methods annotated with `@PostConstruct` (annotations)
- `afterPropertiesSet()` as defined by the `InitializingBean` callback interface (использовался в Spring 2)
- A custom configured `init()` method (xml)

The JSR-250 `@PostConstruct` and `@PreDestroy` annotations are generally considered best practice for receiving lifecycle callbacks in a modern Spring application.

We recommend that you do not use the `InitializingBean`(`afterPropertiesSet()`) and `DisposableBean` interface, because it unnecessarily couples the code to Spring. 

3. **_postProcessAfterInitialization()_** — вызывается после init() метода.




Destroy methods are called in the same order:

1.  Methods annotated with `@PreDestroy`
    
2.  `destroy()` as defined by the `DisposableBean` callback interface
    
3.  A custom configured `destroy()` method


____ 
### Links
 - https://www.youtube.com/watch?v=BmBr5diz8WA&t=231s (главный спикер)
 лекция с видео в формате статей:
- https://medium.com/@kirill.sereda/spring-%D0%BF%D0%BE%D0%B4-%D0%BA%D0%B0%D0%BF%D0%BE%D1%82%D0%BE%D0%BC-9d92f2bf1a04
- https://habr.com/ru/post/222579/