#Install Docker image with Node version 14, which includes both Node.js and npm 
FROM node:14

#This environment variable configures Instana, 
#a monitoring tool, to automatically profile the application. 
#It helps to track the application's performance and behavior in real-time.
ENV INSTANA_AUTO_PROFILE true

#exposes port 8080
EXPOSE 8080

#Sets the working directory to /opt/server
WORKDIR /opt/server

#The package.json file is copied into the container, 
#and npm install is executed to install all the dependencies defined in package.json
COPY package.json /opt/server/

RUN npm install

#This copies the application code (server.js) into the container's /opt/server directory.
COPY server.js /opt/server/

#default command to run 
#when the container starts is node server.js, which starts the Node.js application.
CMD ["node", "server.js"]

