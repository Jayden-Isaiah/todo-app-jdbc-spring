# Dockerfile

# ÉTAPE 1: Build Maven
FROM maven:3.8.7-jdk-17 AS build

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline

COPY src ./src

RUN mvn clean package -DskipTests [cite: 31]

# ÉTAPE 2: Image Finale pour l'Exécution
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]