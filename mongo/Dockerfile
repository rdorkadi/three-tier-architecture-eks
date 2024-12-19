#Installs official MongoDB image with version 5
FROM mongo:5

#copies all .js files from the current directory on your local machine
#to the /docker-entrypoint-initdb.d/ directory inside the container.
COPY *.js /docker-entrypoint-initdb.d/

