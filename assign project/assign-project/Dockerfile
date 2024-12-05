# Use the official Maven image as the base image
FROM maven:3.8.6-openjdk-17 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the Maven project files to the working directory
COPY pom.xml .
COPY src ./src

# Build the application (you can specify the profile, like -Pprod, if needed)
RUN mvn clean package -DskipTests

# Use a lighter image for the runtime environment
FROM openjdk:17-jdk-slim

# Set the working directory in the container
WORKDIR /app

# Copy the built JAR file from the build image
COPY --from=build /app/target/my-app-1.0-SNAPSHOT.jar /app/my-app-1.0-SNAPSHOT.jar

# Expose the port the app will run on (adjust as per your app's requirement)
EXPOSE 8080

# Command to run the JAR file
CMD ["java", "-jar", "/app/my-app-1.0-SNAPSHOT.jar"]
