# Optimizing Images

* Simple Fastapi application
[Refer Here](https://github.com/rithwiksrivastav4/SimpleFastAPI/blob/main/README.md) for steps

* Required:
  * python 3.13
* Steps:
  * copy code
  * install dependencies
  * Expose port
* How to run Appl uvicorn main:app --host 0.0.0.0 --port 8000 --reload
* [Refer Here](https://github.com/dummyrepos/SimpleFastAPI/commit/d8d130a149675862244de5e3dc1bd1184393119a) for first version of Dockerfile
* [Refer Here](https://github.com/dummyrepos/SimpleFastAPI/commit/d0e876352d9a030f1e01705922c45207630bb277) for change to slim version
* [Refer Here](https://github.com/dummyrepos/SimpleFastAPI/commit/b2f56b74739ea07a9e9ac848b62ae19a519dba4f) for changes to use a non root user
* When we tried as a non root user, we are getting permission issues
* [Refer Here](https://github.com/dummyrepos/SimpleFastAPI/commit/acfc848f3352324a22e7a03531c8c9ab4bda184d) for the possible solution where we build dependencies in one stage and copy them into other with permissions to the user

## Simple Spring boot (Java) application

* Existing Dockerfile

```bash
FROM eclipse-temurin:17-jre
ADD https://khajareferenceapps.s3.ap-south-1.amazonaws.com/spring-petclinic-3.2.0-SNAPSHOT.jar /spc.jar
EXPOSE 8080
CMD  ["java", "-jar", "/spc.jar"]
```

* We are building the jar file seperately and using them in Docker Image building process.
* The idea is to build the jar and use the jar as part of Docker Image building itself

## Multi stage Dockerfiles

* This is inspired from a builder pattern
[Refer Here](https://github.com/rithwiksrivastav4/docker-spring-petclinic) for multistage docker for spring petclinic

```bash
FROM maven:3.9-eclipse-temurin-17 AS builder
# build the java code
COPY . /spc
WORKDIR /spc
RUN mvn package
# this will create a spring petclinic jar file


FROM eclipse-temurin:17-jre AS runner
COPY --from=builder --chown=ubuntu /spc/target/spring-petclinic-3.3.0-SNAPSHOT.jar /app/spring-petclinic.jar
USER ubuntu
WORKDIR /app
EXPOSE 8080
CMD ["java", "-jar", "spring-petclinic.jar"]
```
