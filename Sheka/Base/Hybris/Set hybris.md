10.05.2022  10:26
Tags:  |
____

# Set hybris

Если у вас до этого была установлена java 7 или 8 версии с помощью установщика, то удалите Java приложения из Apps Windows.  
  
Скачайте Full JDK 8 по https://libericajdk.ru/pages/downloads/  
для windows  
положить разархивированную папку в C:\Program Files\Java  
зайти в переменные среды  
![[Pasted image 20220510110831.png]]  
добавить переменную JAVA_HOME  
Variable name: JAVA_HOME  
Variable value: your_java_path (например: C:\Program Files\Java\bellsoft-jdk8u332+9-windows-amd64-full\jdk8u332-full)  
Настроить переменную PATH  
![[Pasted image 20220510111617.png]]  
  
проверить правильную установку java можно в консоли c помощью java -version, посмотреть правильно ли проложен путь where java  
![[Pasted image 20220510113255.png]]  
  
Затем продолжить инициализацию проекта по шагам https://confluence.komus.net/pages/viewpage.action?spaceKey=OWT&title=Initialization+Hybris+Komus52  
  
Дополнительные шаги:  
при возникновении во время сборки (gradlew clean all) ошибок maven попробовать следующие шаги:  
1. Очистить .m2/repository.  Настроить settings.xml как в "Дополнительные шаги" https://confluence.komus.net/pages/viewpage.action?spaceKey=OWT&title=Initialization+Hybris+Komus52  
2. Установить с помощью внешнего maven'а проблемные зависимости "mvn dependency:get -Dartifact=com.sun.org.apache.xml.internal:resolver:20050927 && mvn dependency:get -Dartifact=javax.jws:jsr181-api:1.0-MR1 && mvn dependency:get -Dartifact=org.codehaus.woodstox:woodstox-core-asl:4.2.0 && mvn dependency:get -Dartifact=org.glassfish.gmbal:gmbal-api-only:3.1.0-b001".  
3. В чистой рабочей копии проекта запустить "gradlew clean all".





____ 
### Links
-