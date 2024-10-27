# First stage: build the application
FROM maven:3.8.6-eclipse-temurin-17 AS build

# Set the working directory
WORKDIR /app

# Copy only the pom.xml and download dependencies
COPY StayEase/pom.xml ./
RUN mvn dependency:go-offline -B

# Copy the rest of the application source code
COPY StayEase/src ./src

# Build the application
RUN mvn clean package -DskipTests

# Second stage: create a lightweight runtime image
FROM eclipse-temurin:21-jre-jammy

# Set the working directory
WORKDIR /app

# Copy the JAR file from the build stage
COPY --from=build /app/target/Stay-Ease-0.0.1-SNAPSHOT.jar app.jar

# Expose the application port (optional, adjust based on your app)
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "app.jar