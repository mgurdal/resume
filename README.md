# Personal Web Page

This is the material template for my personal web page. 

If you want to create a page similar to this, you can clone the repository and follow the steps below.

## Setup

Install the required dependencies.

```bash
pip install mkdocs==1.1 mkdocs-material==5.0.1
```

## Serve

Serve the web page on local.

```bash
mkdocs serve
```

## Deploy

Deploy the changes to the **gh-pages** branch. 

```bash
mkdocs serve
```

You can also setup a workflow in order to automate this process.

This is a basic workflow to deploy your master branch to gh-pages.

```yaml
name: CI

# Controls when the action will run. Triggers the workflow on push or pull request events but only for the master branch
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
    - uses: actions/checkout@v2

    # Install mkdocs and build the page 
    - name: Build
      run: | 
        sudo apt-get install python3-setuptools
        python3 -m pip install mkdocs mkdocs-material
        python3 -m mkdocs build

    # Deploy to the gh-branch using the GITHUB_TOKEN.
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./site
        publish_branch: gh-pages  # deploying branch
```