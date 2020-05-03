# 1.13
# Build and run the Docker image:
# docker build -t my-java-app .
# docker run -d -p 8080:8080 --rm --name my-running-app my-java-app
# OR
# docker run -it -p 8080:8080 --rm --name my-running-app my-java-app


# https://hub.docker.com/_/openjdk
FROM openjdk:8
EXPOSE 8080

# https://github.com/docker-hy/spring-example-project

RUN pwd
# ---> /

# Build app on a host machine (laptop): ./mvnw package

# Adds a file from the same location where Dockerfile is
COPY ./spring-example-project/ /usr/src/myapp

# create and set the current working directory to /myapp after this directive
WORKDIR /usr/src/myapp
RUN pwd
#  ---> /usr/src/myapp
RUN ls -al
# ---> same as content of /spring-example-project/

# Optionally (in case if not built on laptop):
# RUN ./mvnw package

RUN ls -al ./target/
# ---> -rw-rw-r--. 1 root root 18225397 Jan 23 15:10 docker-example-1.1.3.jar

ENTRYPOINT ["java", "-jar"] 
# command represents an argument list for the entrypoint
CMD ["./target/docker-example-1.1.3.jar"]
# Unrecognized option: -jar ./target/docker-example-1.1.3.jar
# Error: Could not create the Java Virtual Machine.
# Error: A fatal exception has occurred. Program will exit.
