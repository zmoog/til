# how to install dependencies from git

Sometimes you want to install a Python package from a branch or a specific commit.

Install che `refurbished` package from its GitHub repository, branch `zmoog/loosen-setup-requirements`:

```
$ pip install git+https://github.com/zmoog/refurbished.git@zmoog/loosen-setup-requirements#egg=refurbished
Collecting refurbished
  Cloning https://github.com/zmoog/refurbished.git (to revision zmoog/loosen-setup-requirements) to /private/var/folders/kf/3wt1srds50v37j0z6c7m1kg40000gn/T/pip-install-4n6s0d4p/refurbished_02ff96664da94ca3a4bfa495b0caa2be
  Running command git clone --filter=blob:none --quiet https://github.com/zmoog/refurbished.git /private/var/folders/kf/3wt1srds50v37j0z6c7m1kg40000gn/T/pip-install-4n6s0d4p/refurbished_02ff96664da94ca3a4bfa495b0caa2be
  Running command git checkout -b zmoog/loosen-setup-requirements --track origin/zmoog/loosen-setup-requirements
  Switched to a new branch 'zmoog/loosen-setup-requirements'
  Branch 'zmoog/loosen-setup-requirements' set up to track remote branch 'zmoog/loosen-setup-requirements' from 'origin'.
  Resolved https://github.com/zmoog/refurbished.git to commit 871feb67a479d3a02083440554112716648c59d5
  Preparing metadata (setup.py) ... done
Requirement already satisfied: beautifulsoup4>=4.9.3 in ./venv/lib/python3.9/site-packages (from refurbished) (4.10.0)
Requirement already satisfied: requests>=2.25.1 in ./venv/lib/python3.9/site-packages (from refurbished) (2.27.1)
Requirement already satisfied: price-parser>=0.3.3 in ./venv/lib/python3.9/site-packages (from refurbished) (0.3.3)
Requirement already satisfied: click>=7.1.2 in ./venv/lib/python3.9/site-packages (from refurbished) (8.0.4)
Requirement already satisfied: soupsieve>1.2 in ./venv/lib/python3.9/site-packages (from beautifulsoup4>=4.9.3->refurbished) (2.3.1)
Requirement already satisfied: attrs>=17.3.0 in ./venv/lib/python3.9/site-packages (from price-parser>=0.3.3->refurbished) (21.4.0)
Requirement already satisfied: idna<4,>=2.5 in ./venv/lib/python3.9/site-packages (from requests>=2.25.1->refurbished) (3.3)
Requirement already satisfied: certifi>=2017.4.17 in ./venv/lib/python3.9/site-packages (from requests>=2.25.1->refurbished) (2021.10.8)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in ./venv/lib/python3.9/site-packages (from requests>=2.25.1->refurbished) (1.26.8)
Requirement already satisfied: charset-normalizer~=2.0.0 in ./venv/lib/python3.9/site-packages (from requests>=2.25.1->refurbished) (2.0.12)
Using legacy 'setup.py install' for refurbished, since package 'wheel' is not installed.
Installing collected packages: refurbished
  Attempting uninstall: refurbished
    Found existing installation: refurbished 0.7.1
    Uninstalling refurbished-0.7.1:
      Successfully uninstalled refurbished-0.7.1
  Running setup.py install for refurbished ... done
Successfully installed refurbished-0.7.1
```

