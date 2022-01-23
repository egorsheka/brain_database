26.12.2020  13:39
Tags: #dev  | #job 
____

# Multi-stage builds

![[Pasted image 20201226133948.png]]
Если Dockerfile состоит из нескольких билдов, то в итоговый image будут записанны данные только из последнего билда (на картинке из второго). Чтобы обратится к данным прошло билда необходиму использовать параметр --from=nameOfTheBuild 

Для java это можно использовать для сборки приложений с помощью maven или gradle
```
FROM maven:3.6.3-jdk-11 AS build  
RUN mkdir -p /workspace  
WORKDIR /workspace  
COPY pom.xml /workspace  
COPY src /workspace/src  
RUN mvn -f pom.xml clean package  
  
FROM openjdk:11  
COPY --from=build /workspace/target/*.jar app.jar  
EXPOSE 8080  
ENTRYPOINT ["java","-jar","app.jar"]
```
____ 
### Links
- [[Docker]]