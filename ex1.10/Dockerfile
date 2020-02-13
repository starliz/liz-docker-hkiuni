# 1.10
# Command to build and tag/name: 
# docker build -t run110 .
# Command to run container (in detached mode and remove after use): 
# docker run -d --rm -p 5000:5000 run110  // --rm option may be used to clean the garbage after
# Run the container with -p <host-port>:<container-port>  so Docker will map containers ports to host (your machine) ports. 


FROM ubuntu:16.04 
#FROM node:12-alpine --- another option

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs 

# --- by adding the instructions to the bottom we preserve our cached layers --- 

# Exposing port - tell Docker that the container listens to a certain port
EXPOSE 5000

WORKDIR /usr/src/app
#COPY ./frontend-example-docker/package*.json ./
COPY ./frontend-example-docker/ ./
RUN npm install
RUN npm audit fix
RUN npm install -g serve

#just to see what's there
RUN ls -al /usr/src/app

# The CMD represents an argument list for the entrypoint. By default entrypoint is set as /bin/sh and this is passed if no entrypoint is set. 
# There are two ways to set them: exec form and shell form. 
# We’ve been using the exec form where the command itself is executed. 
ENTRYPOINT ["npm"] 
CMD ["start"]
