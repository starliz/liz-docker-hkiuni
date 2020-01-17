# Command to build and tag/name: docker build -t myfirst . 

# Specify the base image
FROM ubuntu:16.04 

# It is better to put heavy processing commands in the beginning, so they wouldn't run every time when you rebuild image.

# If we add another package in the apt-get install -y line some other day, 
# the sources might have changed and thus the installation will fail. 
# When something depends on another command, it’s best practise to run them together.
RUN apt-get update -y && apt-get -y install wget


# Create and set the current working directory to /mydir after this directive
WORKDIR /mydir 

# Execute a command with /bin/sh -c
RUN touch hello.txt 

# Adds a file from the same location where Dockerfile is
COPY local.txt . 


RUN wget http://example.com/index.html 

# This will be executed when using "docker run"
CMD ["/bin/bash"]