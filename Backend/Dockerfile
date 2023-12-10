#FROM maven:3.8.4-openjdk-17-slim as stage1
#WORKDIR /opt/demo
#COPY pom.xml .
#RUN mvn dependency:go-offline
#COPY ./src ./src
#RUN mvn clean install -Dmaven.test.skip=true
#
#
#FROM eclipse-temurin:17-jdk-alpine
#WORKDIR /opt/demo
#COPY --from=stage1 /opt/demo/target/demo.jar /opt/demo
#EXPOSE 8080
#ENTRYPOINT ["java", "-jar", "app.jar"]



#1st phase
FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /app
COPY pom.xml .
COPY src src
RUN mvn clean package -DskipTests
#2nd phase
FROM eclipse-temurin:17.0.9_9-jre-ubi9-minimal
WORKDIR /app
COPY --from=build /app/target/spring-boot-data-jpa-0.0.1-SNAPSHOT.jar /app/app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]