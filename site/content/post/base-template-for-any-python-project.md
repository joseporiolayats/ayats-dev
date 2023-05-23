---
title: Base template for any Python project
date: 2023-05-23T10:11:57.268Z
description: This is the basic steps in order to create a reproducible,
  flexible, adaptable environment for any kind of python project that has venv
  and package management using Poetry
---
# Base Template for Python 3.11 Project

## Project Structure

* Create a new directory for your project.
* Initialize a new Git repository in the project directory.

## Poetry Setup

* Install Poetry: `pip install poetry`
* N﻿avigate into the directory of the project or create it
* Activate the virtual environment: `poetry shell`
* Initialize a new Poetry project: `poetry init`
* Follow the prompts to configure your project.

```yaml
[tool.poetry]
name = "project_name"
version = "0.1.0"
description = "project_description"
authors = \["joseporiolayats <oriol.ayats@gmail.com>"]
license = "MIT"
readme = "README.md"
documentation = "https://joseporiolayats.github.io/my-github-repo"
repository = "https://github.com/joseporiolayats/my-github-repo"
keywords = ["tag1,"tag2","tag3"]
packages = [{include = "project_name" }]

[tool.poetry.dependencies]
python = "^3.11"
colorlog = "^6.7.0"
python-decouple = "^3.8"
pymdown-extensions = "^10.0.1"

[tool.poetry.group.test.dependencies]
ruff = "^0.0.269"
pytest = "^7.3.1"
pytest-asyncio = "^0.21.0"

\[tool.poetry.group.docs.dependencies]
mkdocs = "^1.4.3"
mkdocs-material = "^9.1.14"
mkdocstrings-python = "^1.0.0"

\[tool.poetry.group.linst.dependencies]
black = "^23.3.0"

\[build-system]
requires = \["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

## Dependencies and Environment Management

* Add project dependencies to `pyproject.toml` using the `[tool.poetry.dependencies]` section.
* Install the project dependencies: `poetry install`
* Update dependencies: `poetry update`

## Version Control with GitHub

* Create a new repository on GitHub.
* Link the local Git repository to the remote repository: `git remote add origin <repository-url>`
* Push the initial code to the remote repository: `git push -u origin main`

## Code Quality and Pre-commit

* Install pre-commit: `pip install pre-commit`
* Create a `.pre-commit-config.yaml` file in the project root.
* Configure pre-commit hooks to enforce code quality checks.
* Run `pre-commit install` to enable the pre-commit hooks.

## Project Documentation

* Generate API documentation using tools like Sphinx or MkDocs.
* Add documentation files to the project, such as `README.md` and `docs/`.
* Write clear and concise documentation for your project.

## Continuous Integration and Testing

* Set up continuous integration using tools like GitHub Actions or Travis CI.
* Create test cases using a testing framework like PyTest.
* Configure CI workflows to run tests automatically on every push.

## Project Management and Task Tracking

* Utilize project management tools like GitHub Projects or Trello.
* Create tasks and track progress to stay organized.
* Collaborate with team members effectively.