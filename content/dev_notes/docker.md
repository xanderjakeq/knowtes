---
title: "docker"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- tool
---

[website](https://www.docker.com/)

Docker is a tool that makes setting up environments for software to run
on any platform reliably. It does this by packaging the source code along 
with all its dependencies defined in a [[dev_notes/Dockerfile]].

Multiple [[dev_notes/docker image]]s can be used to create multi-container applications
using [[dev_notes/docker-compose]].


[src](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)
kill all running containers:
```
$ docker kill $(docker ps -q)
```

remove exited containers:
```
$ docker rm $(docker ps -a -f status=exited -q)
```

delete all images
```
$ docker rmi $(docker images -a -q)
```
