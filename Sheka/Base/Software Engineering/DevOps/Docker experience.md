24.12.2020  20:42
Tags: #dev | #job 
____

# Docker examples
---

## Main commands

images:
```
docker images 		all of images
docker rmi 			delete image
```

containers:
```
docker run name 	runs new container
docker ps			all of containers
docker rm			remove container 
docker logs			to see logs if container runs in deamon
```
---
## Dockerfile

### SpringBoot

```
FROM maven:3.6.3\-jdk-11 AS build  
RUN mkdir \-p /workspace  
WORKDIR /workspace  
COPY ../../../../pom.xml /workspace  
COPY ../../.. /workspace/src  
RUN mvn \-f pom.xml clean package  
  
FROM openjdk:11  
COPY --from=build /workspace/target/\*.jar app.jar  
EXPOSE 8080  
ENTRYPOINT \["java","-jar","app.jar"\]
```

### mysql
```
FROM mysql:8  
ENV MYSQL_DATABASE sheka  
ENV MYSQL_USER sheka  
ENV MYSQL_PASSWORD sheka  
  
COPY createdb.sql /docker-entrypoint-initdb.d/  
  
HEALTHCHECK --interval=5s CMD mysql -uroot-p${MYSQL_ROOT_PASSWRD} -e "SHOW DATABASES;"
```

``docker build -t name .``
``docker run -it -d -e MYSQL_ROOT_PASSWORD=root task4``
```
docker exec -it eb6 bash
		mysql -uroot -p;
		show databases;
		use table;
		select * from table;
```

---

Если использовать в своём image oracle JDK, то есть вероятность, что Docker может удалить с Hub наш image, поэтому используется openJDK.
![[Pasted image 20201224215652.png]]
Каждый docker image имеет свою ОС. Для JDK лучше всего подойдёт alpine, т.к. она наиболее минималистична.
____ 
### Links
- [[Docker experience]]
-  [[Docker]]