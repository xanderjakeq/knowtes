---
title: "node garbage collection"
enableToc: false
date: "2023-08-10"
lastmod: :git
tags:
- js
- node
---
```js
import { setFlagsFromString } from 'v8'; 
import { runInNewContext } from 'vm'; 

setFlagsFromString('--expose_gc'); 
const gc = runInNewContext('gc'); // nocommit gc();
```
https://stackoverflow.com/questions/27321997/how-to-request-the-garbage-collector-in-node-js-to-run