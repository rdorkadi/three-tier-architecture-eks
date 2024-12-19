#Installs official MySQL 5.7 image as the base image
FROM mysql:latest

#This command defines a mount point for data inside the container at /data. 
#It ensures that any data written to this directory persists even if the container is deleted, 
#and it can be shared with other containers or the host machine.
VOLUME /data

#These environment variables set MySQL's initial configuration:
#MYSQL_ALLOW_EMPTY_PASSWORD=yes: This allows MySQL to start without 
 #requiring a password for the root user (not recommended for production).
#MYSQL_DATABASE=cities: Creates a database named cities upon initialization.
#MYSQL_USER=shipping: Creates a user named shipping.
#MYSQL_PASSWORD=secret: Sets the password for the shipping user.
ENV MYSQL_ALLOW_EMPTY_PASSWORD=yes \
    MYSQL_DATABASE=cities \
    MYSQL_USER=shipping \
    MYSQL_PASSWORD=secret

# change datadir entry in /etc/mysql/my.cnf
COPY config.sh /root/
RUN /root/config.sh

#copies all scripts from the scripts/ 
#directory on the host machine into the /docker-entrypoint-initdb.d/
COPY scripts/* /docker-entrypoint-initdb.d/

#RUN /entrypoint.sh mysqld & while [ ! -f /tmp/finished ]; do sleep 10; done
#RUN rm /docker-entrypoint-initdb.d/*

