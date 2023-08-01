---
title: "packaging into an appimage"
enableToc: false
date: "2023-07-31"
lastmod: :git
tags: 
- appimage
- native
---
Distribute a project using an [[dev_notes/appimage|appimage]] to linux users.
Install [appimage-builder](https://appimage-builder.readthedocs.io/en/latest/intro/install.html) and [linuxdeploy](https://github.com/linuxdeploy/linuxdeploy).

define a `.desktop` file:
```
[Desktop Entry]
Name=project_name
Exec=binary_file_name
Icon=icon_name // without file extension
Type=Application
Categories=Utility // not sure if this is arbitrary
```

create an `AppDir` using linux deploy:
```
linuxdeploy -e target/release/binary --appdir binary.AppDir -i icon.png -d binary(project name).desktop
```

if there are any static files needed for the project, copy them into the `AppDir/usr/bin` 
directory.
```
cp other_bin ./binary.AppDir/usr/bin/other_bin
cp models/ ./binary.AppDir/usr/bin/models/ -r
```

then, create the appimage:
```
linuxdeploy --appdir $app_dir --output appimage
```


## Note:
The generated appimage is readonly. If the project needs to write files, make sure
to write using absolute paths in application code to the user's `$HOME` directory.
Create `$HOME/.project_name` directory to contain all generated files.


