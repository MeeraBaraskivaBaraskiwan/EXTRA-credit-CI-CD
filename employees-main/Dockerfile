# Stage 1: build the JAR
FROM maven:3.9.9-eclipse-temurin-21-alpine AS build
WORKDIR /app

# 1) copy the POM
COPY pom.xml .

# 2) copy the Checkstyle config (so the plugin can find it)
COPY checkstyle.xml .

# 3) copy your source code
COPY src ./src

# 4) now run Maven (it will find checkstyle.xml under /app)
RUN mvn clean package -DskipTests

# Stage 2: run the JAR
FROM eclipse-temurin:21-jdk-alpine
VOLUME /tmp
ARG JAR_FILE=target/*.jar
COPY --from=build /app/${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]