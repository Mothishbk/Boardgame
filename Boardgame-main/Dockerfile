# ---------- Stage 1: BUILD (Maven + JDK compile the JAR) ----------
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests
# produces target/*.jar

# ---------- Stage 2: RUNTIME (small JRE runs the JAR) ----------
FROM eclipse-temurin:17-jre
WORKDIR /app

# copy ONLY the built JAR out of the build stage
COPY --from=build /app/target/*.jar app.jar

# run as a non-root user, not root
RUN useradd -m appuser
USER appuser

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
