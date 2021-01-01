# Setting up MKDocs

## Pre-requisite

Setup local working environment

```
> home dir
cd Tools
python3 -m venv $HOME/Tools/.venv
source $HOME/Tools/.venv/bin/activate

python3 -m pip install --requirement=Documents/GitHub/Documents/requirements.txt

// Enterprise option
python3 -m pip install --index-url=https://nexus.com/repository/pypi-proxy/simple \
    --trusted-host=nexus.com \
    --index=https://nexus.com/repository/pypi-proxy/pip \
    --requirement=requirements.txt

python3 -m pip install mkdocs-git-revision-date-localized-plugin==0.5.2

python3 -m pip install mkdocs-redirects

pip install mkdocs-minify-plugin

python3 -m mkdocs serve

Open http://127.0.0.1:8000
```
