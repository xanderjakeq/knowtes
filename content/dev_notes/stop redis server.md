---
title: stop redis server
enableToc: false
date: 2025-06-23
lastmod: :git
tags:
  - linux
---
While working on a project, I needed to run a docker image of redis. But somehow there's always an instance running taking up the default redis port.

For some reason linux has a redis-server that stays up and when I kill the process it just starts another one. I saw that this can be disabled but I'm not sure what's depending on it and I don't want to break things.

```
sudo systemctl disable redis-server
```
[source](https://askubuntu.com/a/898198)

I just opted to remap the port to my host with docker. `-p 6380:6379`

```
docker run \
  -p "6380:6379" \
  -d \
  --name "redis_$(date '+%s')" \
  redis:7

```