# Use the official Gradle image to build the application.
# This is the build stage.
FROM gradle:8.5-jdk17 AS build
WORKDIR /home/gradle/src
COPY build.gradle settings.gradle ./
COPY gradle ./gradle
COPY --chown=gradle:gradle . .
# Build the application, creating the executable JAR file.
RUN gradle build --no-daemon

# Use a smaller base image for the final container.
# This is the final stage.
FROM openjdk:17-jdk-slim
# Argument to specify the path to the JAR file.
ARG JAR_FILE=build/libs/*.jar
# Copy the JAR file from the build stage.
COPY --from=build /home/gradle/src/${JAR_FILE} app.jar
# Expose the port the application runs on.
EXPOSE 8080
# The command to run the application.
ENTRYPOINT ["java","-jar","/app.jar"]
