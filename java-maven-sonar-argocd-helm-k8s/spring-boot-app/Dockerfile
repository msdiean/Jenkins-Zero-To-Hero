# ======== Stage 1: Build the JAR using Maven =========
FROM maven:3.8.5-openjdk-17-slim AS build

WORKDIR /app

# Copy only pom.xml first to leverage Docker cache
COPY pom.xml .

# Download dependencies
RUN mvn dependency:go-offline

# Now copy the rest of the project
COPY src ./src

# Package the application
RUN mvn clean package -DskipTests

# ======== Stage 2: Run the app with a lightweight JRE =========
FROM eclipse-temurin:17-jre-alpine

WORKDIR /opt/app

# Copy the jar file from the build stage
COPY --from=build /app/target/*.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]
