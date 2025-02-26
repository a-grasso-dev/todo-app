# Étape 1 : Construction avec Maven
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app

# Copier le fichier pom.xml pour télécharger les dépendances
COPY pom.xml ./
RUN mvn dependency:go-offline -B

# Copier le code source et compiler le projet
COPY src ./src
RUN mvn clean package -DskipTests

# Étape 2 : Image de production avec OpenJDK (plus légère)
FROM openjdk:17-jdk-slim
WORKDIR /app

# Copier le fichier .jar généré de l'étape de construction
COPY --from=build /app/target/todo-app-0.0.1-SNAPSHOT.jar app.jar

# Exposer le port de l'application
EXPOSE 8080

# Lancer l'application
CMD ["java", "-jar", "app.jar"]
