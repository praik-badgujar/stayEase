# Use a base image with Maven to build the project
FROM maven:3.8.6-eclipse-temurin-17 AS build

# Set the working directory
WORKDIR /app

# Copy the project files into the container
COPY . .

# Package the application using Maven
RUN mvn clean package

# Use a lightweight Java image to run the application
FROM eclipse-temurin:21-jre-jammy

# Set the working directory
WORKDIR /app

# Copy the jar file from the build stage
COPY --from=build /app/target/Stay-Ease-0.0.1-SNAPSHOT.jar app.jar

# Command to run the application
CMD ["java", "-jar", "app.jar"]