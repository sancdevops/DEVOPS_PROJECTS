# Stage 1: Build the Java application using Maven
FROM maven:3.8.4-openjdk-11 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean install

# Stage 2: Run SonarQube scan
FROM sonarsource/sonar-scanner-cli:4.6 AS sonar-scan
WORKDIR /app
COPY --from=build /app/target/my-java-app-1.0-SNAPSHOT.jar .
RUN sonar-scanner \
  -Dsonar.host.url=http://your-sonarqube-server:9000 \
  -Dsonar.login=your-sonarqube-token \
  -Dsonar.projectKey=my-java-app \
  -Dsonar.sources=src \
  -Dsonar.java.binaries=target

# Optionally, you can use a smaller base image for the final production image
# Stage 3: Create the production image
FROM openjdk:11-jre-slim
WORKDIR /app
COPY --from=sonar-scan /app/my-java-app-1.0-SNAPSHOT.jar .
CMD ["java", "-jar", "my-java-app-1.0-SNAPSHOT.jar"]

