#base image
FROM nginx:1.21.6

#tells Docker that the container will listen on port 8080
EXPOSE 8080

#These environment variables define host names for different service 
#components of an application. These variables can be used in configuration files or 
#scripts to configure the various backend services that Nginx will route to, 
#such as catalogue, user, cart, shipping, payment, and ratings
ENV CATALOGUE_HOST=catalogue \
    USER_HOST=user \
    CART_HOST=cart \
    SHIPPING_HOST=shipping \
    PAYMENT_HOST=payment \
    RATINGS_HOST=ratings 

#The COPY command copies the entrypoint.sh script into the container. 
#The ENTRYPOINT instruction sets this script to run when the container starts. 
#This script could be used to perform custom startup 
#tasks such as setting up configuration files based on environment variables.
COPY entrypoint.sh /root/
ENTRYPOINT ["/root/entrypoint.sh"]

#This command copies a Nginx configuration template into the container. 
#This template can be used to dynamically generate an actual Nginx configuration based on 
#environment variables or other configuration files when the container starts.
COPY default.conf.template /etc/nginx/conf.d/default.conf.template

#This copies static content (e.g., HTML, CSS, JS files) 
#from the host machine into the default web directory of Nginx (/usr/share/nginx/html
COPY static /usr/share/nginx/html
