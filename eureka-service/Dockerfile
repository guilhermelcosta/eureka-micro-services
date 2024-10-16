FROM ubuntu:latest AS build

RUN apt-get update
RUN apt-get install openjdk-21-jdk -y
COPY ../../.. .

RUN apt-get install maven -y
RUN mvn clean install

FROM openjdk:21-jdk-slim

EXPOSE 8761

COPY --from=build target/eureka-service-0.0.1-SNAPSHOT.jar app.jar
COPY --from=build src/main/resources/application.yml application.yml

LABEL authors="Guilherme Costa"

ENTRYPOINT ["java", "-jar", "app.jar"]
