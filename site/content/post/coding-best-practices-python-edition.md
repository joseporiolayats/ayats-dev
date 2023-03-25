---
title: Coding Best Practices - Python Edition
date: 2023-03-25T09:33:20.220Z
description: How to know if code is well written, structured, readable and will
  stand the test of time? Following this general set of rules will ensure that
  best practices are implemented and so the code will be of high quality.
image: img/3296882916_a_python_snake_typing_code_in_front_of_a_laptop__concept_art__photorealistic__hq__4k.png
---
1. Create a Code Repository and use Version Control
2. Create Readable Documentation
3. Follow Style Guidelines
4. Correct Broken Code Immediately
5. Use the PyPI Instead of Doing it Yourself
6. Use the Right Data Structures
7. Write Readable Code
8. Use Virtual Environments
9. Write Object-Oriented Code
10. What Not to Do while Programming in Python

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

Additionally, and much recommended, is to use a widespread and trustworthy structure with **\*cookiecutter**.*

The documentation can be found [here.](https://cookiecutter.readthedocs.io/en/stable/)

An example use for Data Science projects in general goes like this ([by cookiecutter data-science](https://github.com/drivendata/cookiecutter-data-science)):

```
cookiecutter -c v1 https://github.com/drivendata/cookiecutter-data-science
```

And results in a project structure like this:

```
├── LICENSE
├── Makefile           <- Makefile with commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default Sphinx project; see sphinx-doc.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
├── src                <- Source code for use in this project.
│   ├── __init__.py    <- Makes src a Python module
│   │
│   ├── data           <- Scripts to download or generate data
│   │   └── make_dataset.py
│   │
│   ├── features       <- Scripts to turn raw data into features for modeling
│   │   └── build_features.py
│   │
│   ├── models         <- Scripts to train models and then use trained models to make
│   │   │                 predictions
│   │   ├── predict_model.py
│   │   └── train_model.py
│   │
│   └── visualization  <- Scripts to create exploratory and results oriented visualizations
│       └── visualize.py
│
└── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io
```

``

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

The code that doesn't work should never be pushed into the main development branch. 

Instead, when a broken path is detected, one should open a PR, branch the code at that point, and fix it ASAP. Then petition to merge it into the main development branch.

This methodology is effective at protecting the main development timeline and is called "Zero defects methodology".

## 5. Use Available Packages

The main power of Python is the widespread availability and ease of use of its infinite packages with infinite use-cases.

![pypi](img/pypi_logo.svg.png "Python Package Index pypi")

So whenever you need some special and repeatable method, first take a look around because chances are that someone faced it before... and packaged the solution. 

So don't waste your time.

Use PyPI, conda, github... but don't re-write.

## 6. Data Structures

In python there are several data structures, and each one is better suited for different use-cases. Choosing badly will lead to slow performance or maybe major re-writing of the code.

![https://www.edureka.co/blog/wp-content/uploads/2019/10/TreeStructure-Data-Structures-in-Python-Edureka1.png](img/treestructure-data-structures-in-python-edureka1.png "Python Data Structures from edureka")

Always take into account the general data structures as well as user or package created ones:

* List
* Tuple
* Dictionary
* Set

## 7. Readable Code

If you follow PEP8 convention then you're almost there. 

Also, the code has to be easy to understand. Without unused imports or methods, only necessary comments, keep all the comments with the same style, maximum line length set at 79 or 80 chars.

Variable names should be descriptive for anyone even without reading the rest of the code.

```python
# Don't write like this
x = 1
y = 2

def my_function(a,b):
    z = a * b
    return z

compute = my_function(x,y)
print("Result is: ",compute)

#
# Should be LIKE THIS
#
heigth = 1
width = 2

def area_rectangle(side_a:float,side_b:float)->float:
    """
    Returns the area of a rectangle in float by
    entering both sides and multiplying them.

    :param side_a: Length of the first side
    :param side_b: Lenght of the second side
    :return: The computed area.
    :rtype: float

    """
    return a*b
  
area = area_rectangle(heigth,width)
print(f"The rectangle has {area} sqm")
```

And yes, [f'strings](https://www.geeksforgeeks.org/formatted-string-literals-f-strings-python/) are very useful for that matter!

## 8. Virtual Environments

One virtual environment for every project. This is a golden rule. Every project starts with the virtual env creation.

![virtual envs venv](img/python-venv-explained-header.png "Python virtual environments")

There are many options for that matter:

* [venv](https://docs.python.org/3/library/venv.html)
* [pipenv](https://pipenv-es.readthedocs.io/es/latest/)
* [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html)
* [poetry](https://python-poetry.org/)

The reason behind virtual environments is avoiding package collisions and keeping configurations local.

This makes the code reproducible and so, reliable.

## 9. Be Object-Oriented

There is good reason to not have everything in one file with thousands of functions. 

![Python objects](img/python-object-oriented-programming-inheritance-schema.png "Object relationship")

Python is a very good object-oriented easy to understand language. In order to exploit this feature, one should code taking into account that:

* Every function should do exactly one thing
* Every class should be focused on a single multi-stage task
* Every file (module) should contain all the methods related to the same process.
* Every package should be a collection of all the methods required for the task the package is aimed to solve.

By using this principle it is really easy to make object-oriented code reusable, readable, modular, encapsulated, and inheritable.

## 10. What to Avoid

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



# Wrapping up

Writing good python code is easy and achievable if one follows a simple set of rules.

In this article I presented my general rules for that purpose, but there may be others. 

This is the foundation of the checks needed for MLOps, Data Science, DevOps and general python coding.