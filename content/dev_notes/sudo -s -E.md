---
title: sudo -s -E
enableToc: false
date: 2023-05-05
lastmod: :git
tags:
  - linux
  - cli
---
Spawn a `sudo` shell while preserving the current environment.

beware when creating files. it will have conflicting permissions
when editing without elevated permissions. something about
`read-only file`
