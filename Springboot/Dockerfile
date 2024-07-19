
##     TEST get github and buid    ##
#FROM maven:3.8.5-openjdk-11 AS build
#RUN apt-get update && apt-get install -y git
#WORKDIR /app
#RUN git clone https://github.com/JoaoNeto4/helpdesk-backend .
#RUN mvn clean package -DskipTests
#FROM openjdk:11-jre-slim
#WORKDIR /app
#COPY --from=build /app/target/*.jar app.jar
#EXPOSE 8080
#ENTRYPOINT ["java", "-jar", "app.jar"]


FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src

RUN mvn clean package -DskipTests

FROM openjdk:17-jdk-slim
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]