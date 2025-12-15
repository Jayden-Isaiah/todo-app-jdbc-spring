# Dockerfile (Mise à jour pour Java 25)

# ÉTAPE 1: Build Maven
FROM maven:latest-jdk-25 AS build 
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# ÉTAPE 2: Image Finale pour l'Exécution
FROM eclipse-temurin:25-jre-alpine 
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]