31.01.2021  17:06
Tags: #dev  | #job 
 ____

# Java Persistence

## Terminology

**JDBC** (Java DataBase Connection) — это стандарт низкого уровня для взаимодействия с базами данных с использованием чистого SQL.
Проблема JDBC заключается в огромном количестве кода, где самой бизнес-логики будет 15%.

**ORM** (Object-Relational Mapping) —  это технология программирования, которая позволяет автоматически  сохранять объекты в таблицах базы данных SQL с использованием правил, прописанных разработчиком. Т.е. предоставляет мепинг из объектно-ориентированных систем в реляционные модели данных. 

**JPA** - java спецификация, которая реализует концепцию **ORM**.

**Hibernate** - самая популярная реализация спецификации **JPA**

**Spring Data** - Это библиотека/фреймворк, который добавляет дополнительный уровень абстракции поверх JPA.

----

@Embeddable в книге 123 страница 









JPA или Hibernate?
Hibernate развивается намного быстрее. Есть некторые вещи, которые есть в Hibernate, но не вошли в JPA: Identifier generators Formulas Immutable entities Entity-level caching Multi-tenancy Dynamic inserts/updates. Например анотации создания и удаления.

Слоёность Persistence:
![[Pasted image 20210131173624.png]]

В сравнении (миграция с Hibernate  на JPA очень проста)
![[Pasted image 20210131173718.png]]
---- 



## Hibernate 
? прочекать последнее поле в инете
? посмотреть возможности диалекта 
![[Pasted image 20210131174417.png]]

### @GeneratedValue
параметры | значения
------------------ | -------------------------
**table** | основана на отдельной таблице, не используется
**auto** | выбирается оптимальная стратегия для используемой базы данных
**sequence** | рекумендуется, дает лучшее преимущество в производительности, инкрементирует на всю БД
**identity** |  инкрементируется на одну таблицу 
**UUID** | гарантирует, что значение будет единсвенным во всей вселенной

Пятый вариант переопределить генерацию самому:
![[Pasted image 20210131213905.png]]
![[Pasted image 20210131213914.png]]
![[Pasted image 20210131213933.png]]


-----
### Атрибуты для @Column
![[Pasted image 20210131184443.png]]

--------------------------
## Enum to Database
![[Pasted image 20210131185034.png]]
Всегда лучше использовать втлорой вариант, потому что если удалится один из элементов в enum, то проблме не возникнет. Но лучше всего переопределить метод, тогда и поиск будет быстрее и не будет проблем в дальнейшем возможном удалении.
![[Pasted image 20210131185623.png]]
![[Pasted image 20210131185638.png]]

--------------------------
В ситуации, когда целесобразно заменить String на Boolean, например Yes и No, то есть на это конвертре.

![[Pasted image 20210131185835.png]]



```java
@CreatedDate  
private LocalDateTime created;  
  
@LastModifiedDate  
private LocalDateTime modified;
```

![[Pasted image 20210131223203.png]]
--------------------------

## Другие возможности








![[Pasted image 20210219184556.png]]

https://www.jug.ch/events/slides/170221_High-Performance-Hibernate-Ch-JUG.pdf

https://vladmihalcea.com/14-high-performance-java-persistence-tips/
____ 
### Links!
[[Java Persistence API and Hibernate.pdf]]
- https://www.youtube.com/watch?v=C-wEZjEOhWc
- https://dzone.com/articles/what-is-the-difference-between-hibernate-and-sprin-1
- https://www.youtube.com/watch?v=nwM7A4TwU3M&list=RDCMUCYrGYT7BswsJGkmG7-IAF8g&index=5

