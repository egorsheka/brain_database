09.02.2021  22:11
Tags: #dev | #job 
____

# Associations
## Встраиваемые классы

```java
@Embeddable
public class Address {

	@NotNull Игнорируется при генерации DDL 
	@Column(nullable = false) Используется при генерации DDL 
	protected String street; 
	@NotNull 
	@Column(nullable = false, length = 5) Переопределяет VARCHAR(255) 
	protected String zipcode; 
	@NotNull
	@Column(nullable = false) 
	protected String city;
}
```
![[Pasted image 20210209222240.png]]

```java
@Entity 
@Table(name = "USERS") 
public class User implements Serializable { 

	@Id 
	protected Long id;
	protected Address homeAddress;
}
```
5.2 раздел книги [[Java Persistence API and Hibernate.pdf]] (более подобно про переопределение полей)

-----------
## Отображение наследования
### 1. MappedSuperclass. Одна таблица для каждого конкретного класса и неявный полиморфизм
```java
@MappedSuperclass
```
![[Pasted image 20210210100525.png]]

```sql
select ID, OWNER, ACCOUNT, BANKNAME, SWIFT from BANKACCOUNT
select ID, CC_OWNER, CARDNUMBER, EXPMONTH, EXPYEAR from CREDITCARD
```
Применять этот подход (только) для верхушки иерархии классов, где полиморфизм на самом деле не нужен(нельзя, чтобы User имел поля BillingDetails) и не предвидится изменений в суперклассе в будущем(будут сложности с переменованием полей).
 


## 2. TABLE_PER_CLASS. Одна таблица для каждого конкретного класса с объединениями
```java
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS) 
```
Таблица выглядит точно также, как прошлом примере
```java
@Entity  
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)  
public abstract class BillingDetails  {  
    @Id  
 	@GeneratedValue(strategy = GenerationType.SEQUENCE)  
    protected Long id;  
 	@NotNull  
 	protected String owner;  
}
```
```sql
select ID, OWNER, EXPMONTH, EXPYEAR, CARDNUMBER, ACCOUNT, BANKNAME, SWIFT, CLAZZ_ 
from (
	select ID, OWNER, EXPMONTH, EXPYEAR, CARDNUMBER, 
	null as ACCOUNT, 
	null as BANKNAME, 
	null as SWIFT, 
	1 as CLAZZ_ from CREDITCARD 
		union all 
			select id, OWNER,
			null as EXPMONTH, 
			null as EXPYEAR, 
			null as CARDNUMBER,
			ACCOUNT, BANKNAME, SWIFT,
			2 as CLAZZ_ from BANKACCOUNT 
	) as BILLINGDETAILS
```
Таблицы объединяются с помощью оператора UNION, а в промежуточный результат вставляются литералы (в данном случае это 1 и 2); они нужны фреймворку Hibernate для создания экземпляра правильного класса.

Преимуществом является возможность применения полиморфных ассоциаций; например, теперь стало возможным отобразить ассоциацию от класса User к классу BillingDetails. Но невозможно применить стратегию 
```java
@GeneratedValue(strategy = GenerationType.IDENTITY)
```

## 3. SINGLE_TABLE. Единая таблица для целой иерархии классов
```java
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
```
![[Pasted image 20210210122136.png]]
```sql
select 
ID, OWNER, EXPMONTH, EXPYEAR, CARDNUMBER, ACCOUNT, BANKNAME, SWIFT, BD_TYPE
from BILLINGDETAILS
#Для выполнения запроса к подклассу CreditCard Hibernate
#добавит ограничение на столбец селектора: 
select 
ID, OWNER, EXPMONTH, EXPYEAR, CARDNUMBER
from BILLINGDETAILS where BD_TYPE=’CC’
```

Данная стратегия отображения – лучшая с точки зрения производительности и простоты. Это самый производительный способ представления полиморфизма – как полиморфные, так и неполиморфные запросы работают быстро, – и можно с легкостью писать запросы вручную. Можно получать отчеты на основе произвольных запросов, не применяя сложных соединений или объединений. Эволюция схемы происходит довольно просто.

Но есть одна главная проблема – целостность данных. Столбцы для свойств, объявленных в подклассах, могут содержать null. Если каждый подкласс объявляет несколько свойств, которым нельзя присваивать null, отказ от ограничения NOT NULL может стать серьезной проблемой с точки зрения корректности данных. Другой проблемой является нормализация: данная стратегия создает функциональные зависимости между простыми столбцами, нарушая третью нормальную форму.



## 4. JOINED. Одна таблица для каждого подкласса с использованием соединений
```java
@Inheritance(strategy = InheritanceType.JOINED)
```
Результатом получится 3 таблицы, причем первичный ключ таблицы-родителя будет совпадать с ключами дочерних таблиц.
![[Pasted image 20210210125601.png]]
```sql
select 
	BD.ID, BD.OWNER, 
	CC.EXPMONTH, CC.EXPYEAR, CC.CARDNUMBER,
	BA.ACCOUNT, BA.BANKNAME, BA.SWIFT, 
	case
		when CC.CREDITCARD_ID is not null then 1
		when BA.ID is not null then 2 
		when BD.ID is not null then 0 
	end
from 
	BILLINGDETAILS BD
	left outer join CREDITCARD CC on BD.ID=CC.CREDITCARD_ID
	left outer join BANKACCOUNT BA on BD.ID=BA.ID
#Для более простого запроса к подклассу, такого как select cc from CreditCard cc,
#Hibernate использует внутреннее соединение:
select 
	CREDITCARD_ID, OWNER, EXPMONTH, EXPYEAR, CARDNUMBER
from 
	CREDITCARD
	inner join BILLINGDETAILS on CREDITCARD_ID=ID
```
Главное преимущество этой стратегии заключается в нормализации схемы SQL. Эволюция схемы и определение ограничений целостности осуществляются довольно просто. Внешний ключ, ссылающийся на таблицу конкретного подкласса, может представлять полиморфную ассоциацию с этим конкретным подклассом.

Более того, хотя эта стратегия кажется простой, наш опыт говорит, что для сложных иерархий классов производительность может оказаться неприемлемой. Запросы требуют соединения нескольких таблиц или многих последовательных операций чтения.

## Какую стратегию выбрать? Ответ в 6.7 [[Java Persistence API and Hibernate.pdf]]
----
Выберите подходящую реализацию и сразу же инициализируйте коллекцию; поступая так, вы избегаете появления неинициализированных коллекций. Мы не советуем инициализировать коллекции позже, в конструкторах или методах записи. Вот типичный пример объявления параметризованного множества (Set):
```java
Set images = new HashSet();
```
---
##  Relationships (best practices)
### @OneToOne


____ 
### Links
-