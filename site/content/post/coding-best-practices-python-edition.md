---
title: Coding Best Practices - Python Edition
date: 2023-03-25T09:33:20.220Z
description: How to know if code is well written, structured, readable and will
  stand the test of time? Following this general set of rules will ensure that
  best practices are implemented and so the code will be of high quality.
image: img/3296882916_a_python_snake_typing_code_in_front_of_a_laptop__concept_art__photorealistic__hq__4k.png
---
1. Create a Code Repository and Implement Version Control
2. Create Readable Documentation
3. Follow Style Guidelines
4. Correct Broken Code Immediately
5. Use the PyPI Instead of Doing it Yourself
6. The Zen of Python
7. Use the Right Data Structures
8. Write Readable Code
9. Use Virtual Environments
10. Write Object-Oriented Code
11. What Not to Do while Programming in Python

\  

## 1. VCS - Version Control System

Version Control is critical for good tracking of each code modification and it's really good when working in conjunction with other developers.

Version control is handled with git . The implementation can be local, in-house or cloud.

For cloud the most popular platforms are:

* [Github](www.github.com)
* [GitLab](www.gitlab.com)
* [Bitbucket](www.bitbucket.com)

Every project should contain the code files and additional markdown files in an understable structure. The minimum is:

* src/ folder
* docs/ folder
* test/ folder
* requirements.txt
* \_\_init\_\_.py, main.py, setup.py
* license file
* README.md

Additionally, and much recommended, is to use a widespread and trustworthy structure with ***cookiecutter**.*

The documentation can be found [here.](https://cookiecutter.readthedocs.io/en/stable/)



## 2. Documentation

Every project needs some form of documentation. Even inline comments are the bare minimum, but one should expect to fulfill at least some docstrings inside classes and methods.

The recommended use-case is Sphinx or MkDocs, making it auto-deployable using CI/CD tools like Github Actions.

```python
def get_random_ingredients(kind=None):
    """
    Return a list of random ingredients as strings.

    :param kind: Optional "kind" of ingredients.
    :type kind: list[str] or None
    :raise lumache.InvalidKindError: If the kind is invalid.
    :return: The ingredients list.
    :rtype: list[str]

    """
    return ["shells", "gorgonzola", "parsley"]
```

Links:

* [Sphinx](www.sphinx-doc.org)
* [MkDocs](mkdocs.org)



## 3. Style Guidelines

In Python there is one standard above all:

[PEP8](https://peps.python.org/pep-0008/)

Every programmer needs to know how to properly write Python code by following the PEP8 convention.

![Python PEP8](img/6519207182729216.png "Python PEP8")

There are a number of tools to check that at the testing stage, using pre-commit hooks with black and flake8 will ensure only PEP8 compliant code will get commited, else it will throw an error and point it out. 

![Pre-commit workflow for Python](img/precommit_pipeline.png "Pre-commit workflow for Python")

Other tools are integrated in major IDEs like PyCharm or VSCode.

## 4. Correct Broken Code

## 5. Use Available Packages

## 6. The Zen of Python

## 7. Data Structures

## 8. Readable Code

## 9. Virtual Environments

## 10. Be Object-Oriented

## 11. What to Avoid

* Import **only the needed methods**, not all of them! You will avoid crashes, name collisions, better use of memory and speed. And it is also a good security measure.

  ```python
  # This is bad
  from sklearn.metrics import *

  # This good
  from sklearn.metrics import confusion_matrix

  # Also this is good practice
  # importing multiple methods at once
  from sklearn.metrics import confusion_matrix, \\
  accuracy_score, f1_score
  ```
* Do **not turn off error reporting** while coding and testing. This should be avoided for obvious reasons. Only turning it off in production code when the errors are known and do not affect the actual product.

  ```python
  # Never do it like this
  import warnings
  warnings.filterwarnings("ignore")
  ```
* Use ***distutils* for altering path** variables
* Handle **secret keys and sensitive information** using an external package, **never hard-encode them** in your python files!\
   Several packages do this: ***python-dotenv*** , *AWS's boto3, Hashicorp's hvac*, etc.\
   \
   Example with *python-dotenv*:\

  1. Create a .**env** file and write inside the key-value pairs.

     ```
       API_KEY=test-key
       API_SECRET=test-secret
     ```
  2. Add the **.env** file in the **.gitignore** file.

  3. In the ***main.py*** file, import and load the **dotenv** package with each secret by the key. The value will be passed through the secure package.

     ```python
     from dotenv import load_dotenv
     import os

     load_dotenv()

     api_key = os.getenv("API_KEY")
     api_secret = os.getenv("API_SECRET")

     print("API_KEY: ", api_key)
     print("API_SECRET: ", api_secret)

     ```

This post is heavily inspired by:

[https://data-flair.training/blogs/python-best-practices](https://data-flair.training/blogs/python-best-practices/)[](https://medium.com/coriers/mlops-best-practices-59c0348e7125)

<https://medium.com/coriers/mlops-best-practices-59c0348e7125>