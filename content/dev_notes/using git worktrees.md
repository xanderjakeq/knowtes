---
title: using git worktrees
enableToc: false
date: 2024-10-31
lastmod: :git
tags:
  - git
  - workflow
---
worktrees allow you to check out multiple branches at the same time.
it is nice when you want to refer to content not available on the 
current branch you are working on

the repo structure should look:
```
project/
	project.git
	main(worktree)
	feat-1(worktree)
```

each worktree is a different branch and can be viewed independently!
`git` commands can only be ran within the worktrees or in the .git directory. 
now you don't change branches with `checkout`, just `cd` into the worktree


## creating from scratch
[source](https://stackoverflow.com/a/7632497)

```
mkdir project
cd project
git init --bare project.git
cd project.git

git worktree add ../main (creates a worktree from branch main or creates branch if doesn't exist)
cd ../main
```

## cloning 
```
mkdir project
cd project
git clone remoterepo --bare 


cd project.git

git worktree add ../main 
cd ../main
```

## turning "normal" repo into bare
[source](https://stackoverflow.com/a/38760153)

```
mkdir worktree_project
cd worktree_project

git clone --mirror ../project_repo_path ./project.git

// rename worktree_project to project
cd ..
rm -rf project
mv ./worktree_project ./project

cd project
git worktree add ../main 
cd ../main
```