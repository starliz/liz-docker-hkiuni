# 1.8
# Command to build and tag/name: docker build -t myfirst .
# docker build -t youtube-dl .
# Command to run container (interactive and remove after use): docker run -it myfirst  // --rm option may be used to clean the garbage after
# docker run youtube-dl

# When you use a bind mount, a file or directory on the host machine is mounted into a container. Bind mounts rely on the host machine’s filesystem having a specific directory structure available.
# When you use a volume, a new directory is created within Docker’s storage directory on the host machine, and Docker manages that directory’s contents.
#  -v creates a directory if the file does not exist.
# docker run -v $(pwd):/mydir youtube-dl https://imgur.com/JY5tHqr
# it downloads the file with success, but: find: ‘*JY5tHqr.mp4’: No such file or directory

FROM ubuntu:16.04 

WORKDIR /mydir 
RUN apt-get update && apt-get install -y wget 

# RUN touch hello.txt 
# COPY local.txt . 
# RUN wget http://example.com/index.html  

# --- by adding the instructions to the bottom we preserve our cached layers --- 

RUN apt-get install -y curl python 
RUN curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl 
RUN chmod a+x /usr/local/bin/youtube-dl 
ENV LC_ALL=C.UTF-8 

# The CMD represents an argument list for the entrypoint. By default entrypoint is set as /bin/sh and this is passed if no entrypoint is set. 
# This is why giving path to a script file as CMD works: you’re giving the file as a parameter to /bin/sh.
ENTRYPOINT ["/usr/local/bin/youtube-dl"]
CMD ["/usr/local/bin/youtube-dl"]


# There are two ways to set them: exec form and shell form. 
# We’ve been using the exec form where the command itself is executed. 
# In shell form the command that is executed is wrapped with /bin/sh -c  --- "-c" option means "command"
