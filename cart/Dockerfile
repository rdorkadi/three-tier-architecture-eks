#Downloads node:14 image for build stage
FROM node:14 AS build

#sets the working directory to /opt/server for consistency during the build.
WORKDIR /opt/server

#Copies package.json into the build context to ensure 
#dependencies are installed based on the application requirements.
COPY package.json /opt/server/

#Installs only the production dependencies, 
#excluding development dependencies, which keeps the final image lightweight.
RUN npm install --only=production

#Copies the application source code into the image for building.
COPY server.js /opt/server/

#Uses a smaller node:14-slim image for the runtime environment to minimize the final image size.
FROM node:14-slim AS runtime

#Sets an environment variable required by the application.
ENV INSTANA_AUTO_PROFILE true

#Declares that the container will listen for incoming traffic on port 8080.
EXPOSE 8080

#Sets the working directory for running the application.
WORKDIR /opt/server

#Ensures that the runtime environment is prepared by 
#installing only the necessary dependencies for the production stage.
RUN npm install

#Copies the built application, 
#including dependencies and code, from the build stage to the runtime stage.
COPY --from=build /opt/server /opt/server

#Specifies the command to run the application when the container starts.
CMD ["node", "server.js"]

