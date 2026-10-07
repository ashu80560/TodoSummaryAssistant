# =========================
# Stage 1: Build
# =========================
FROM maven:3.9.9-eclipse-temurin-17 AS build

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline -B

COPY src ./src

RUN mvn clean package -DskipTests -B


# =========================
# Stage 2: Runtime
# =========================
FROM eclipse-temurin:17-jre-jammy

WORKDIR /app

# Create non-root user
RUN groupadd --system spring && \
    useradd --system --gid spring spring

COPY --from=build /app/target/*.jar app.jar

RUN chown spring:spring /app/app.jar

USER spring

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
