# 1.07
# Command to build and tag/name: docker build -t curler .
# Command to run container (interactive and remove after use): docker run -it --rm curler
# And the optput will be:
# [liz@localhost ex1.07]$ docker run -it --rm curler
# Input website:
# helsinki.fi
# Searching..
# <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
# <html><head>
# <title>301 Moved Permanently</title>
# </head><body>
# <h1>Moved Permanently</h1>
# <p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
# </body></html>
# [liz@localhost ex1.07]$ 


# The base image:
FROM ubuntu:latest

# If we add another package in the apt-get install -y line some other day, 
# the sources might have changed and thus the installation will fail. 
# When something depends on another command, it’s best practise to run them together.
RUN apt-get update -y && apt-get -y install curl

# Create and set the current working directory to /mydir after this directive
WORKDIR /mydir 

# Adds a file from the same location where Dockerfile is
COPY script.sh .

# This will be executed when using "docker run"
CMD ["/bin/bash"]
CMD ["./script.sh"]
