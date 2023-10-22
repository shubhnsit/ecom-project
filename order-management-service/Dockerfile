# Use the official maven/Java image to create a build artifact.
FROM maven:3.8.3-jdk-17 as builder

# Set the working directory in docker
WORKDIR /app

# Copy the pom.xml file into the working directory in docker
COPY pom.xml .

# Download project dependencies (this enhances caching)
RUN mvn dependency:go-offline -B

# Copy the rest of the files into the working directory in docker
COPY src ./src/

# Build the application
RUN mvn package -DskipTests

# Use the official OpenJDK 17 slim image as a runtime base image
FROM openjdk:17-slim

# Set deployment directory
WORKDIR /app

# Copy the jar file from the builder stage to the current directory
COPY --from=builder /app/target/order-management-service-0.0.1-SNAPSHOT.jar /app/order-management-service.jar

# Expose server port (assuming default 8080, change if different)
EXPOSE 8080

# Set the command to run the application
ENTRYPOINT ["java", "-jar", "/app/order-management-service.jar"]
