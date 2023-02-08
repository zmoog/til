Sometimes I need a small CLI tool to interact with some web service. I usually leverage Simon Willison's work, but I have to look for the exact steps every time.

Having a short guide to bootstrap a new CLI tool would be great. 

This is that guide.

***

The starting point is the repo template: https://github.com/simonw/click-app.

The first step is to install [cookiecutter](https://cookiecutter.readthedocs.io/), the tremendous templating tool.

pipx is a great tool to install Python-based CLI tools in isolated environments:

    pipx install cookiecutter
    
Create a new project using https://github.com/simonw/click-app as a template:

```
$ cookiecutter gh:simonw/click-app
You've downloaded /Users/zmoog/.cookiecutters/click-app before. Is it okay to delete and re-download it? [yes]:
app_name []: telegram-cli
description []: Python CLI tool and library for sending messages to Telegram
hyphenated [telegram-cli]:
underscored [telegram_cli]:
github_username []: zmoog
author_name []: Maurizio Branca
```

Set up a virtual env:

```shell
python -m venv venv
. venv/bin/activate
```

Install the package:

```shell
$ pip install -e '.[test]'
Obtaining file:///Users/zmoog/code/projects/zmoog/telegram-cli
  Preparing metadata (setup.py) ... done
Collecting click
  Using cached click-8.1.3-py3-none-any.whl (96 kB)
Collecting pytest
  Using cached pytest-7.2.1-py3-none-any.whl (317 kB)
Collecting exceptiongroup>=1.0.0rc8
  Using cached exceptiongroup-1.1.0-py3-none-any.whl (14 kB)
Collecting attrs>=19.2.0
  Using cached attrs-22.2.0-py3-none-any.whl (60 kB)
Collecting iniconfig
  Using cached iniconfig-2.0.0-py3-none-any.whl (5.9 kB)
Collecting packaging
  Using cached packaging-23.0-py3-none-any.whl (42 kB)
Collecting tomli>=1.0.0
  Using cached tomli-2.0.1-py3-none-any.whl (12 kB)
Collecting pluggy<2.0,>=0.12
  Using cached pluggy-1.0.0-py2.py3-none-any.whl (13 kB)
Installing collected packages: tomli, pluggy, packaging, iniconfig, exceptiongroup, click, attrs, telegram-cli, pytest
  Running setup.py develop for telegram-cli
Successfully installed attrs-22.2.0 click-8.1.3 exceptiongroup-1.1.0 iniconfig-2.0.0 packaging-23.0 pluggy-1.0.0 pytest-7.2.1 telegram-cli-0.1.0 tomli-2.0.1

[notice] A new release of pip available: 22.2.2 -> 23.0
[notice] To update, run: pip install --upgrade pip
```

Run a quick test:

```shell
$ telegram-cli --version
telegram-cli, version 0.1.0
```

Create the GitHub repo and push:

```shell
$ gh repo create zmoog/telegram-cli --public
✓ Created repository zmoog/telegram-cli on GitHub

$ git remote add origin git@github.com:zmoog/telegram-cli.git

$ g push origin main
Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 10 threads
Compressing objects: 100% (13/13), done.
Writing objects: 100% (16/16), 6.84 KiB | 2.28 MiB/s, done.
Total 16 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:zmoog/telegram-cli.git
 * [new branch]      main -> main
 
 Ready to go!

https://github.com/zmoog/telegram-cli
