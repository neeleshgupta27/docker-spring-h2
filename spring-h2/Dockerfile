FROM openjdk:8

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

ENTRYPOINT ["java","-jar","/code/target/spring-h2-0.0.1-SNAPSHOT.jar"]