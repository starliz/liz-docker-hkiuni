# liz-docker-hkiuni
https://devopswithdocker.com/part1/

https://hub.docker.com/repository/docker/starliz/lizlamp

# Part 1

## Exercise 1.4
docker pull devopsdockeruh/exec_bash_exercise

docker run -d --name ex14 devopsdockeruh/exec_bash_exercise
```
    PS C:\Users\LidZale> docker exec -it ex14 bash
    root@df9f3c4c0c30:/usr/app# tail -f ./logs.txt
    Wed, 15 Jan 2020 14:07:42 GMT
    Wed, 15 Jan 2020 14:07:45 GMT
    Secret message is:
    "Docker is easy"
    Wed, 15 Jan 2020 14:07:51 GMT
```

## Exercise 1.5
docker run -it --name ubu-it ubuntu:xenial sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'

docker start ubu-it

docker exec -it ubu-it bash
```
    apt-get update
    apt install curl
    sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
```

## Exercise 1.6 
To build and tag/name: docker build -t docker-clock . 

To run container and clock: docker run docker-clock

To stop: docker stop bold_ardinghelli (container name)

## Exercise 1.7
To build and tag/name: docker build -t curler .

To run container (interactive and remove after use): docker run -it --rm curler

And the optput will be:
```
    [liz@localhost ex1.07]$ docker run -it --rm curler
    Input website:
    helsinki.fi
    Searching..
    <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
    <html><head>
    <title>301 Moved Permanently</title>
    </head><body>
    <h1>Moved Permanently</h1>
    <p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
    </body></html>
    [liz@localhost ex1.07]$ 
```

## Exercise 1.8
docker run -v $(pwd)/host/path/file.txt:/container/path/logs.txt devopsdockeruh/first_volume_exercise 

```
[liz@localhost ex1.08]$ docker run -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise
(node:1) ExperimentalWarning: The fs.promises API is experimental
Wrote to file /usr/app/logs.txt
Wrote to file /usr/app/logs.txt
Wrote to file /usr/app/logs.txt
Wrote to file /usr/app/logs.txt
[liz@localhost ex1.08]$ ls -l
total 8
-rw-rw-r--. 1 liz liz 1433 Jan 17 17:10 Dockerfile
-rw-rw-r--. 1 liz liz  591 Apr 26 16:52 logs.txt
[liz@localhost ex1.08]$ 
```

## Exercise 1.9 publishing port
To check if port is free
`$ sudo netstat -lntup | grep ":8080"`

```
$ docker run -d -p 8080:80 devopsdockeruh/ports_exercise
$ docker container ls
CONTAINER ID     IMAGE                                  COMMAND                  CREATED             STATUS                    PORTS                     NAMES
990b8158248c     devopsdockeruh/ports_exercise          "npm start"              18 seconds ago      Up 15 seconds             0.0.0.0:32768->8080/tcp   silly_morse
```

access in browser: localhost:8080

`"Ports configured correctly!!"`

## Exercise 1.10 Run the project

### Clone repo on host machine to test the app:
```
[liz@localhost ]$ cd home/liz/edu/IT_edu/docker/devopswithdocker/liz-docker-hkiuni/ex1.10/
[liz@localhost ex1.10]$ git clone git@github.com:docker-hy/frontend-example-docker.git
[liz@localhost ex1.10]$ cd frontend-example-docker/
```
Installing Nodejs
```
sudo dnf install -y gcc-c++ make
curl -sL https://rpm.nodesource.com/setup_12.x | sudo -E bash -
sudo dnf install nodejs
```
Check your installed versions
```
node -v && npm -v
v12.15.0
6.13.4
```
Install all packages with 
```
npm install
npm audit fix
npm run
```
### Build & Run docker container
```
[liz@localhost frontend-example-docker]$ cd ..
[liz@localhost ex1.10]$ docker build -t run110 .
...
Successfully built 7241df2137e0
Successfully tagged run110:latest
```
Navigating to http://localhost:5000 and after a little delay seeing:
```
Part 1
Exercise 1.10: Congratulations! You configured your ports correctly!
```
## Exercise 1.11
Cloning backend repo, running frontend, building and running backend:
```
[liz@localhost ex1.11]$ git clone git@github.com:docker-hy/backend-example-docker.git
[liz@localhost ex1.11]$ docker run -d --rm -p 5000:5000 run110
[liz@localhost ex1.11]$ docker build -t backend111 .
[liz@localhost ex1.11]$ docker run -d --rm -p 8000:8000 -v $(pwd)/logs.txt:/usr/src/app/logs.txt backend111
```
 --> open http://localhost:8000/

 --> Port configured correctly, generated message in logs.txt

## Exercise 1.12
Command to build, tag and run backend: 
```
[liz@localhost ex1.12]$ docker build -f Dockerfile.backend -t backend .
[liz@localhost ex1.12]$ docker run -d --rm -p 8000:8000 -v $(pwd)/logs.txt:/usr/src/app/logs.txt backend
```
 --> open http://localhost:8000/

Command to build, tag and run frontend: 
```
[liz@localhost ex1.12]$ docker build -f Dockerfile.frontend -t frontend .
[liz@localhost ex1.12]$ docker run -d --rm -p 5000:5000 frontend
```
--> open http://localhost:5000/

## Exercise 1.13

Clone project, build the app:
```
[liz@localhost ex1.13]$ git clone git@github.com:docker-hy/spring-example-project.git
[liz@localhost ex1.13]$ cd spring-example-project/
[liz@localhost spring-example-project]$ ./mvnw package
[liz@localhost spring-example-project]$ cd ..

```
Build and run the Docker image:
```
[liz@localhost ex1.13]$ docker build -t my-java-app .
[liz@localhost ex1.13]$ docker run -d -p 8080:8080 --rm --name my-running-app my-java-app
```

## Exercise 1.14

Clone project, build the app:
```
[liz@localhost ex1.14]$ git clone git@github.com:docker-hy/rails-example-project.git
[liz@localhost ex1.14]$ cd rails-example-project
[liz@localhost rails-example-project]$ gem install bundler
[liz@localhost rails-example-project]$ bundle install
```

Build the Docker image,  run container:
```
[liz@localhost ex1.14]$ docker build -t my-rails-app .
[liz@localhost ex1.14]$ docker run -it -p 3000:3000 --rm --name my-running-app my-rails-app
=> Booting Puma
=> Rails 5.2.2.1 application starting in development 
=> Run `rails server -h` for more startup options
Puma starting in single mode...
* Version 3.12.0 (ruby 2.6.0-p0), codename: Llamas in Pajamas
* Min threads: 5, max threads: 5
* Environment: development
* Listening on tcp://0.0.0.0:3000
Use Ctrl-C to stop

```

## Exercise 1.15
The link to the project in docker hub: https://hub.docker.com/repository/docker/starliz/lizlamp

This Docker image with LAMP application is an outcome of exercises done in two different courses.

Instructions: https://starliz.github.io/2017/02/17/h5-lamp-in-docker.html

Original files available at https://github.com/starliz/liz-docker-lamp

### To build and run do:
```
git clone git@github.com:starliz/liz-docker-lamp.git 
cd ./liz-docker-lamp/
docker build -f Dockerfile_lamp -t liz/lamp .
docker run -d -p 8080:80 liz/lamp

```

### Publishing to hub.docker.com
```
docker tag liz/lamp:latest starliz/lizlamp:latest
docker login
docker push starliz/lizlamp:latest
```

