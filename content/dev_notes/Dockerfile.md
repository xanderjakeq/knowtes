---
title: "Dockerfile"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- 
---

[reference](https://docs.docker.com/engine/reference/builder/)

A file for [[dev_notes/docker]] to follow with its `build` command to create a [[dev_notes/docker image]].

Here's an example `Dockerfile` for serving a react app. [source](https://github.com/projectcollection/shwag)
```
# use an image called 'node' from dockerhub and call it 'build-stage'
FROM node AS build-stage 

# create directory called '/app' and set it as the current directory
WORKDIR /app

# Copy files from the local machine to the current directory of the 
# image ('/app')
# COPY local-path image-path
COPY . .

# run commands within the image
RUN npm install && npm run build
RUN npm install -g serve

# copy serve.json from within the image to the dist directory
# the dist directory is created after `npm run build`
RUN cp serve.json ./dist/serve.json

# the commands to run when the docker image is executed
ENTRYPOINT ["serve", "-p", "80", "./dist/"]
```

The rest of the Dockerfile example:
```
#FROM nginx:alpine AS deploy-stage

#WORKDIR /usr/share/nginx/html

#RUN rm -rf ./*

#COPY --from=build-stage /app/dist/ .
#COPY --from=build-stage /app/nginx.conf .

#ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

The above are commented because it was used to serve built react app using [nginx](https://www.nginx.com/) in 
place of [serve](https://www.npmjs.com/package/serve). 

As a single page app, it mounts from `index.html` and uses client-side routing when on a route other than `/`, doing a hard refresh would result in a `404` error since the route doesn't 
exist on the server. The way to fix this is to point all `GET` requests to the server to `/` or serve
the `index.html` file.

I'm sure there's a way to do this in nginx but I don't know it. I don't have much experience
using/configuring nginx but `serve` had an easy way to do it. i just have to define a
`rewrites` property inside `serve.json` ([serve docs](https://github.com/vercel/serve-handler#rewrites-array)).