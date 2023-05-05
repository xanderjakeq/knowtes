---
title: "docker-compose"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- tool
---

[docs](https://docs.docker.com/compose/)

docker-compose is a tool that allows for management of multiple docker
containers. It is basically a [[dev_notes/docker]] container container other subcontainers
that makes it easy for the subcontainers to communicate with each other.
It is written in a `docker-compose.yml`.

```
# docker-compose.yml
version: "3.9"
services: #images to run
  web: #arbitrary name for a service
    build: . #will build the image defined in Dockerfile at the defined path
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine" #use local image if found, else pulls from dockerhub
```

## how to manage a codebase with multiple services

subcontainers are defined as `services` in `docker-compose.yml`. Unless the
codebase is a monorepo, there needs to be a way to update services individually.

a. It could be done in a monorepo, but these could be large. If a developer
only has to work on one of the services, it doesn't make sense to have
them download the rest of the codebase to be able to work. 

b. The solution: make all the services into their own `image` and use the `image`
property for services. This way, the project file for the services doesn't have
to be on the same repository as the `docker-compose.yml` file. If the image
is on [[dev_notes/dockerhub]], you don't even need to have the source code.