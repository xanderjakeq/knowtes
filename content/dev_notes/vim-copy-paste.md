---
title: "vim-copy-paste"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- tool
---
Copying from vim to system clipboard is very useful. It can be tricky though. I only started using it recently, in
reference to today's date: 2022-04-04. 

Some useful links when it stops working:

https://stackoverflow.com/questions/11489428/how-to-make-vim-paste-from-and-copy-to-systems-clipboard
https://vi.stackexchange.com/questions/84/how-can-i-copy-text-to-the-system-clipboard-from-vim
https://github.com/neovim/neovim/wiki/FAQ#how-to-use-the-windows-clipboard-from-wsl

On windows WSL:
[win32yank](https://github.com/equalsraf/win32yank/releases/tag/v0.0.4) needs to be added to `$PATH`. Here's a [guide](https://linuxize.com/post/how-to-add-directory-to-path-in-linux/) to do that.