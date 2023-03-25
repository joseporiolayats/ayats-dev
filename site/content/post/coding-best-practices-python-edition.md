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

## 2. Documentation

## 3. Style Guidelines

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