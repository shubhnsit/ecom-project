# Use the official maven/Java image to create a build artifact.
FROM maven:3.8.3-jdk-17 as builder

# Set the working directory in docker
WORKDIR /app

# Copy the pom.xml file into the working directory in docker
COPY pom.xml .

# Download project dependencies (for caching purposes)
RUN mvn dependency:go-offline -B

# Copy the rest of the files into the working directory in docker
COPY src ./src/

# Package the application
RUN mvn package

# Use the official OpenJDK 17 slim image for a runtime environment with just the JRE installed
FROM openjdk:17-slim

# Set deployment directory
WORKDIR /app

# Copy the jar file from the builder stage to the current directory
COPY --from=builder /app/target/service-registry-app-0.0.1-SNAPSHOT.jar /app/service-registry-app.jar

# Set the command to run the application using the java command
ENTRYPOINT ["java", "-jar", "/app/service-registry-app.jar"]
