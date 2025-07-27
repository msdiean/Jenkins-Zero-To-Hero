# ======== Stage 1: Build the JAR using Maven =========
FROM maven:3.8.5-openjdk-17-slim AS build

WORKDIR /app

# Copy only pom.xml to leverage Docker cache
COPY pom.xml .

# Download dependencies
RUN mvn dependency:go-offline

# Now copy the source code
COPY src ./src

# Package the application (skip tests to speed up)
RUN mvn clean package -DskipTests


# ======== Stage 2: Use custom image to run the app =========
FROM msdiean/spring-app-java17  # Your custom base image

WORKDIR /opt/app

# Copy the JAR from the build stage
COPY --from=build /app/target/*.jar app.jar

# Run the JAR
ENTRYPOINT ["java", "-jar", "app.jar"]
