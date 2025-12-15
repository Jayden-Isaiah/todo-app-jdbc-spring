# Dockerfile

# ÉTAPE 1: Build Maven
FROM maven:3.8.7-jdk-17 AS build
# Définir le répertoire de travail
WORKDIR /app
# Copier le pom.xml pour télécharger les dépendances en premier (mise en cache)
COPY pom.xml .
# Télécharger les dépendances (simule une compilation)
RUN mvn dependency:go-offline
# Copier le reste du code source
COPY src ./src
# Compiler et packager l'application (sauter les tests)
RUN mvn clean package -DskipTests [cite: 31]

# ÉTAPE 2: Image Finale pour l'Exécution
FROM eclipse-temurin:17-jre-alpine
# Définir le répertoire de travail
WORKDIR /app
# Copier le JAR compilé de l'étape de build
COPY --from=build /app/target/*.jar app.jar
# Le port d'écoute est 8080 (par défaut pour Spring Boot) [cite: 55]
EXPOSE 8080
# Commande d'exécution
ENTRYPOINT ["java", "-jar", "app.jar"]