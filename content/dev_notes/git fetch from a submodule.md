---
title: git fetch from a submodule
enableToc: false
date: 2023-12-08
lastmod: :git
tags:
  - git
---
[src](https://stackoverflow.com/questions/58666714/fetching-remote-from-a-submodule-finds-no-branch)

git fetch behaves differently when executed from within a submodule.
`git fetch origin +refs/heads/*:refs/remotes/origin/*