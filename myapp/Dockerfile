#Setting the base image to use for this Java app
FROM openjdk:11-jre-slim AS builder

#setting the working dir 
WORKDIR /app

#copy the JAR file into the docker image
COPY target/*.jar app.jar

#way to pass the version as argument from the cli
ARG VERSION

#Way to set the version as lable
LABEL version=${VERSION}


#change the user to non-root user UID 1000
USER 1000

#expose of the port
EXPOSE 8080

#cmd to run my app
CMD ["java", "-jar", "app.jar"]