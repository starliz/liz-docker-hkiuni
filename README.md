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



----------------------------------------
Publishing to hub.docker.com
----------------------------------------
docker tag liz/lamp:latest starliz/lizlamp:latest
docker login
docker push starliz/lizlamp:latest
