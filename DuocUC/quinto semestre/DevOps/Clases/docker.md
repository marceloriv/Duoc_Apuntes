# Comandos docker

El archivo docker enseñado en clases

## dockerfile

´´´bash
FROM maven:3.9.14-eclipse-temurin-17-alpine AS alpine

WORKDIR /workspace
COPY pom.xml .
COPY src src/
RUN mvm clean package -DskipTests

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

COPY --from=build /workspace/target/*.jar  app.jar

EXPOSE 8080

ENTRYPOINT [ "java","-jar","app.jar" ]

# docker build -t productos

# docker run 8080:8081

´´´

## comandos terminal

 docker -v  
 .\mvnw.cmd clean package
docker build -t productos .\Dockerfile

## docker-compose.yml

´´´text
services:
  postgres:
    image: postgres:15.3
    environment:
      - POSTGRES_USER=myuser
      - POSTGRES_PASSWORD=secret
      - POSTGRES_DB=mydb
    ports:
      - "5432:5432"
    labels:
      org.springframework.boot.jdbc.parameters: "ssl=true&sslmode=require"

´´´
>[!note]
>se esta usando la base de datos postgres