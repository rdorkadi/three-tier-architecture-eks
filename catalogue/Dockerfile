#Uses the full Node.js node:14 image, which is necessary 
#for compiling and building the application.
FROM node:14 AS build

#Sets the working directory to /opt/server where all files will reside during the build.
WORKDIR /opt/server

#Copies package.json into the container and installs only the production dependencies, 
#ensuring a smaller final image by excluding unnecessary development dependencies.
COPY package.json /opt/server/

RUN npm install --only=production

#Copies the application's source code into the container, 
#making it ready for execution in the next stage.
COPY server.js /opt/server/

#Switches to a lighter base image, node:14-slim, 
#to optimize the size of the final runtime container.
FROM node:14-slim AS runtime

#Adds a non-root user (non-root) 
#to improve security by avoiding running the application as the root user.
RUN useradd -m -s /bin/bash non-root && \
apt-get update && \
apt-get install -y sudo && \
usermod -aG sudo non-root && \
echo "non-root ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

#Switches to the non-root user to run the application, 
#enhancing security by adhering to best practices.
USER non-root

#Sets up an environment variable and 
#exposes port 8080 for the application to listen on. The working directory is also set.
ENV INSTANA_AUTO_PROFILE true

EXPOSE 8080

WORKDIR /opt/server

#opies the built application and all dependencies from the build stage to the runtime stage, 
#ensuring only the necessary files are included in the final image.
COPY --from=build /opt/server /opt/server

#Specifies the command to run the application when the container starts.
CMD ["node", "server.js"]

