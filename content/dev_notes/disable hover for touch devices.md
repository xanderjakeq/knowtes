---
title: "disable hover for touch devices"
enableToc: false
date: "2023-08-23"
lastmod: :git
tags:
- web
- css
---

[src](https://stackoverflow.com/a/64553121)

```css
@media (hover: hover) and (pointer: fine) {
  a:hover { color: red; }
}
```