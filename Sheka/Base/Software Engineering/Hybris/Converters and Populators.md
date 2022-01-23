01.09.2021  09:19
Tags:  |
____

#  Converters and Populators

Converters всегда наследуют AbstractPopulatingConverter
Populators всегда наследуют интерфейс Populator

точка входа метод convert, при этом converter затем использует лист populators
конвертор может содержать в себе дрцгеи конверторы 

Each population step can invoke services or copy data from the source business object to the prototype Facade Data object

Facades always use a Converter to create a new instance of a Data Object prototype and then invoke Populators or other Converters to fulfill the task of building up the Data Object.

## Configurable Populators
The point here is to only convert what is required when it is required by specifying exactly which populators should be used programmatically.
## Function
The basic function of converter is that is create the target object. Inside converter we 

## Flow
The typical flow of program execution within SAP Commerce is this.

Controller —> Facades —> Services —> DAO

- controller
- facade
- convert mapping is given in *facade-spring.xml, we define converter 
...
расписать флоу популятора
...

Почему популяторы вызываются именно с конверторов?
- рекомендация hybris
- таким образом возможно вызывать неграниченное количество популяторов![[Pasted image 20210902112640.png]]
____ 
### Links
-
INSERT_UPDATE Category; code[unique = true]; order; $allowedPrincipals_customergroup; $catalogVersion  
 ; pretplata     ; 0 ;  
 ; pretplata-net ; 1 ;  
 ; kombinuj      ; 2 ;