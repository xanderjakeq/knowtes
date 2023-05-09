---
title: "initializing a 2d array in python"
enableToc: false
date: "2023-05-09"
lastmod: :git
tags:
- py
---

I want to initialize an array like this: `[[0,0],[0,0],...x]`  
```python
arr = [[]] * num
```
This way seem like it works, but the sub-array is only referenced. If you try to append
to a sub array:
```python
arr = [[]] * 2
arr[0].push(1)

# -> [[1],[1]]
```
Every sub-array get's appended to since they're only references to one array.

```python
arr = [[] for i in range(num)]
```
This is the proper way to do it. Every sub-array is a it's own instance.