
---
title: "git submodules subtress"
enableToc: false
tags:
- tool
---
[blog](https://opensource.com/article/20/5/git-submodules-subtrees)
[docs](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

A way to manage cases where a project is needed within another project, and
still be able to treat them as separate git repositories.

```
projectA:
	src:
		main.ts
		etc/
		projectB
```