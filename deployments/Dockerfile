FROM maven:3.6.3-jdk-11-slim AS MAVEN_TOOL_CHAIN

COPY pom.xml /tmp/
WORKDIR /tmp/

RUN mvn dependency:go-offline -B

WORKDIR /

COPY src /tmp/src
WORKDIR /tmp/

RUN mvn package

FROM openjdk:11-jre-slim

COPY --from=MAVEN_TOOL_CHAIN /tmp/target/ingress-mip*.jar /app.jar

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
