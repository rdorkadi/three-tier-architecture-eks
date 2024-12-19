#
# Build

#Install base image that will be used to create container
FROM debian:latest AS build

#Installs Maven, a build automation tool used for Java projects
RUN apt-get update && apt-get -y install maven

#Sets the working directory to /opt/shipping, \
# where all operations like copying files and running commands will occur.
WORKDIR /opt/shipping

#Copies the pom.xml into the working directory.
COPY pom.xml /opt/shipping/

#Resolves and downloads project dependencies based on pom.xml
RUN mvn dependency:resolve

#Copies the source code into the working directory.
COPY src /opt/shipping/src/

#Runs mvn package to compile the source code and package it into a .jar file, 
#which is stored in the target directory.
RUN mvn package

#
# Run
#

#Installs the OpenJDK 8 image, which is used to run the Java application.
FROM openjdk:8-jdk

#Declares that the container will listen on port 8080 for incoming traffic.
EXPOSE 8080

#Sets the working directory to /opt/shipping.
WORKDIR /opt/shipping

#Defines environment variables:
#CART_ENDPOINT: Specifies the endpoint of the cart service.
#DB_HOST: Specifies the hostname of the database.

ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

#Copies the packaged .jar file from the build stage into the runtime stage.
COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

#Runs the Java application with specified JVM options:
#-Xmn256m: Sets the size of the young generation heap to 256 MB.
#-Xmx768m: Sets the maximum heap size to 768 MB.
#-jar shipping.jar: Specifies the .jar file to run.
CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar" ]

