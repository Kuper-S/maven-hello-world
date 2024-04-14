# Stage 1: Build and test the application
FROM maven:3.6.3-openjdk-11 as builder

ARG IMAGE_TAG=latest
#setting the working dir
WORKDIR /app

# Copy the pom.xml and source code
COPY pom.xml .
COPY src ./src

# Compile the application and run tests
RUN mvn clean package

# Stage 2: Create the final Docker image
FROM openjdk:11-jre-slim

WORKDIR /app

RUN useradd --no-log-init -r appuser

# Copy the JAR file from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Use the non-root user to run the application
USER appuser

# Command to run the application
CMD ["java", "-jar", "app.jar"]
