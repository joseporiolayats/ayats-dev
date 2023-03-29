---
title: Documentation - MkDocs & Github Actions
date: 2023-03-29T09:09:14.804Z
description: >-
  Documentaion is the key to enable well mantained - and well used - packages,
  so setting up the right configuration is crucial for that.

  It is an integral part of our MLOps with CI/CD deployment.
image: img/1641394719822.png
---
I'm going to use the **[MKDocs](https://www.mkdocs.org)** package for Python in order to generate a nice documentation site, and by hosting it to github, setting up some [**Github Actions** ](https://github.com/features/actions)in order to make it deploy the documentation automatically and update it at every commit.

**M﻿KDocs** is very helpful because it looks through the actual methods of your package to generate the documentation pages.

S﻿o while doing the methods, one has to take into account to always include [docstrings](https://peps.python.org/pep-0257/) to enable the generation of the documentation.

I﻿'m going to call this example project: **myproject** (hurray for originality!). If you copy some of the code snippets just search and replace myproject entries with your actual project name



S﻿ample code for deploying a github page by using automations from github actions workflow with mkdocs.

m﻿yproject/.github/workflows/mkdocs.yml

```gitconfig
name: Documentation
on:
  push:
    branches:
      - master

# Allow one concurrent deployment
concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  # Build job
  build-deploy:
    name: Build
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Set up python 3
        uses: actions/setup-python@v3
        with:
          python-version: 3.11

      - run: pip install markdown-include
      - run: pip install pymdown-extensions
      - run: pip install mkdocs-material
      - run: pip install mkdocstrings
      - run: pip install mkdocstrings-python
      - run: mkdocs gh-deploy --force --clean
```