---
title: "ubuntu set local time"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- linux
- cli
---

Run this command especially for dual booting with windows to match the time format.
Windows use local time while linux use utc by default. 

This sets linux to also use local time
```
timedatectl set-local-rtc 1 --adjust-system-clock
```