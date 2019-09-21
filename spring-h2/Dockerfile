FROM openjdk:7

RUN apt-get update -qq && apt-get install -y maven && apt-get clean

WORKDIR /code

ADD pom.xml /code/pom.xml
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

RUN ls -lrt /code/target

CMD ["java", "-jar", "target/spring-h2-jar-with-dependencies.jar"]
