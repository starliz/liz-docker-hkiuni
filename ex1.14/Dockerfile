# 1.14
# Build the Docker image:
# docker build -t my-rails-app .
# Run container:
# docker run -it -p 3000:3000 --rm --name my-running-app my-rails-app

# https://hub.docker.com/_/ruby
FROM ruby:2.6.0
EXPOSE 3000

# https://github.com/docker-hy/rails-example-project

# Adds a file from the same location where Dockerfile is
COPY ./rails-example-project/ /usr/src/myapp

# create and set the current working directory to /myapp after this directive
WORKDIR /usr/src/myapp

RUN bundle install 
RUN apt-get update -y && apt-get -y install nodejs
RUN rails db:migrate

ENTRYPOINT ["rails"] 
# command represents an argument list for the entrypoint
CMD ["s"]
