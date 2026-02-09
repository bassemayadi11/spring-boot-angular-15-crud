# ===== Stage 1: Build =====
FROM maven:3.9.6-eclipse-temurin-8 AS build

WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn clean package -DskipTests

# ===== Stage 2: Run =====
FROM eclipse-temurin:8-jre-alpine

WORKDIR /app
COPY --from=build /app/target/spring-boot-jpa-h2-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
