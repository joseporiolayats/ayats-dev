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

```python
from sqlalchemy import create_engine

# Connect to a PostgreSQL database
engine = create_engine('postgresql://username:password@host:port/database_name')

# Execute a SQL query and return the results as a dataframe
query = "SELECT * FROM table_name WHERE column_name > 100"
df = pd.read_sql(query, engine)

# Write a dataframe to a new table in the database
df.to_sql('new_table_name', engine)
```



This post is heavily inspired by:

[https://data-flair.training/blogs/python-best-practices](https://data-flair.training/blogs/python-best-practices/)[](https://medium.com/coriers/mlops-best-practices-59c0348e7125)

<https://medium.com/coriers/mlops-best-practices-59c0348e7125>