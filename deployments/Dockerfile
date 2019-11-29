FROM maven:3.6.2-jdk-11 AS MAVEN_TOOL_CHAIN

COPY pom.xml /tmp/
WORKDIR /tmp/

RUN mvn dependency:go-offline -B

WORKDIR /

COPY src /tmp/src
WORKDIR /tmp/

RUN mvn package

FROM openjdk:11

COPY --from=MAVEN_TOOL_CHAIN /tmp/target/ingress-mip*.jar /app.jar

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
#FROM tomcat:9.0.29-jdk11-openjdk

#COPY --from=MAVEN_TOOL_CHAIN /tmp/target/ingress-mip*.jar $CATALINA_HOME/webapps/ingress-mip.jar