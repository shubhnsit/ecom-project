# Use the official maven/Java image to create a build artifact.
# This is based on Debian and sets up Maven in the /usr/share/maven directory
FROM maven:3.8.3-jdk-17 as builder

# Set the working directory in docker
WORKDIR /app

# Copy the pom.xml file into the working directory in docker
COPY pom.xml .

# This command downloads the project dependencies first (for better caching)
RUN mvn dependency:go-offline -B

# Copy the rest of the files into the working directory in docker
COPY src ./src/

# Package the application
RUN mvn package

# Use the official OpenJDK 17 slim image for a runtime environment with just the JRE installed
FROM openjdk:17-slim

# Set deployment directory
WORKDIR /app

# Copy the jar file from builder to the current location
COPY --from=builder /app/target/auth-service-0.0.1-SNAPSHOT.jar /app/auth-service.jar

# Set the command to run your application using the java command
ENTRYPOINT ["java", "-jar", "/app/auth-service.jar"]
