FROM openjdk:7

RUN apt-get update -qq && apt-get install -y maven && apt-get clean

WORKDIR /code
VOLUME /tmp

ADD pom.xml /code/pom.xml
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

RUN ["ls", "/code/target"]

ARG JAR_FILE
ADD ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]