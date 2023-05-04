---
title: "trunk"
enableToc: false
tags:
- tool
---

https://trunk.io/
Trunk simplifies checking, testing, and merging your code, allowing you to focus on writing features instead of babysitting PRs.

for rust, add 
`.rustfmt.toml`
with content
```
edition = "2021"
```
so it `trunk` doesn't give an error when it finds an `async` function

(haven't used it tho)