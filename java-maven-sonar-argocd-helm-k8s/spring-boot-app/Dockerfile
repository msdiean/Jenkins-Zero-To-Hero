# Use Java 17 (Temurin is the official successor of AdoptOpenJDK)
FROM eclipse-temurin:17-jre-alpine

# Define the artifact path (JAR file)
ARG artifact=target/spring-boot-web.jar

# Set working directory inside the container
WORKDIR /opt/app

# Copy the JAR file to the container
COPY ${artifact} app.jar

# Set the startup command
ENTRYPOINT ["java", "-jar", "app.jar"]
