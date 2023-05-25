---
title: "adding appimages to bin"
enableToc: false
date: "2023-05-13"
lastmod: :git
tags:
- tool
---

[source](https://forums.linuxmint.com/viewtopic.php?t=258314)

Say you have a `nvim.appimage` somewhere. To be able to run it anywhere,
add it to the `/usr/bin` directory.

make it executable.
```
chmod +x program.appImage
```

[symlink](https://linuxize.com/post/how-to-create-symbolic-links-in-linux-using-the-ln-command/) it to `bin`
```
ln -s /path/to/appimage/nvim.appimage /usr/bin/nvim
```
