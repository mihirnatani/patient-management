FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline -B

COPY src ./src

# Build the project and create the executable JAR
RUN mvn clean install -DskipTests

FROM openjdk:21-jdk AS runner

WORKDIR /app

COPY --from=builder ./app/target/patient-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4000

ENTRYPOINT ["java","-jar","app.jar"]


# Steps of what we did here
#1. Use Maven + Java image → build project → produce JAR
#2. Use clean Java image → copy only the JAR → set it up to run
#3. Run the app in Docker container → app is accessible at localhost:4000
