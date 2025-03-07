---
title: process running on port
enableToc: false
date: 2025-03-06
lastmod: :git
tags:
  - linux
---
`sudo ss -lptn 'sport = :8000'`
"ss is used to dump socket statistics"

`ss [options] [filter]`

`sport` means source port. check the man page to find out more