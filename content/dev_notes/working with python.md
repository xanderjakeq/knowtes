---
title: "working with python"
enableToc: false
date: "2023-07-20"
lastmod: :git
tags:
- python
---
version manager: [pyenv](https://github.com/pyenv/pyenv)
environment manager: [virtualenv](https://pyinstaller.org/en/stable/development/venv.html)
package manager: [huak](https://github.com/cnpryer/huak)
- i haven't tested using it yet but looks interesting
bundler: [pyinstaller](https://pyinstaller.org/en/stable/)

pyenv pip problem
https://github.com/pyenv/pyenv-virtualenv/issues/410#issuecomment-1191203446

dev:
```
$ pyenv install [version]
$ pyenv virtualenv [version] [envname]
$ pyenv activate [envname] #could use huak here maybe
(envname)$ pip install [package]
(envname)$ pip install pyinstaller
(envname)$ pip freeze >> requirements.txt
(envname)$ pyenv deactivate
```

packaging:
```
(envname)$ pyinstaller [entryfile] --onefile
```

should output an executable in the dist directory
