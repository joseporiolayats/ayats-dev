---
title: Useful logging in Python
date: 2023-06-08T10:23:16.971Z
description: Logs are the winner approach to know what's going on inside your
  app. Let's configure it to get the best output!
---
## D﻿irectory structure

F﻿or a good logging experience, first of all we need to keep a nice and consistent directory structure.

F﻿ollowing the standard cookiecutter scheme, it should look something like that (notice the logs dirs)

```shell
.
├── my-app
│   ├── app.py
│   ├── database.py
│   ├── **init**.py
│   ├── logs
│   │   ├── logger.py
├── logs
│   ├── my-app.log
├── main.py
├── poetry.lock
├── pyproject.toml
├── README.md
└── tests
```

T﻿he main directory has a **logs** directory which is where the actual `.log` files will be stored.
T﻿he app directory (my-app here) has a **logs** directory with the `logger.py` governing script.

## Logger config

H﻿ere is where the magic happens, for this script will configure the logger module in python.

I﻿n order to log in colors and make them more useful, we're going to use the module colorlog, which can be installed by

```shell
poetry add colorlog
```

H﻿ere I'm pasting my own script with logging colors.

```python
"""
my-app/logs/logger.py

my-app Logging Module

This module sets up loggers for different parts of the graphscraper app. The loggers can
be imported and used in other modules to log messages with different levels of severity.
"""
import logging
import pathlib

import colorlog


def setup_logger(logger_name: str, log_file: str, level: int = logging.INFO) -> logging.Logger:
    """
    Set up a logger with the specified name, log file, and log level.

    Args:
        logger_name (str): The name of the logger.
        log_file (str): The file path where the logger should store logs.
        level (int, optional): The log level. Defaults to logging.INFO.

    Returns:
        logging.Logger: The configured logger instance.
    """

    # Get the absolute path of the 'graphscraper' folder
    base_dir = pathlib.Path(__file__).resolve().parent.parent.parent

    # Create the 'logs' folder if it does not exist
    logs_dir = base_dir / "logs"
    logs_dir.mkdir(exist_ok=True)

    # Get the absolute path of the log file
    log_file_path = logs_dir / log_file

    # Define log colors based on severity
    log_colors = {
        "DEBUG": "white",
        "INFO": "green",
        "WARNING": "yellow",
        "ERROR": "red",
        "CRITICAL": "bold_red",
    }

    logger = logging.getLogger(logger_name)
    logger.setLevel(level)

    # Create a file handler
    file_handler = logging.FileHandler(log_file_path)
    file_handler.setLevel(level)

    # Create a console handler
    console_handler = logging.StreamHandler()
    console_handler.setLevel(level)

    # Use colorlog formatter for console handler
    console_formatter = colorlog.ColoredFormatter(
        "%(log_color)s%(asctime)s - %(name)s - %(levelname)s - %(message)s",
        log_colors=log_colors,
        reset=True,
        style="%",
    )

    console_handler.setFormatter(console_formatter)

    # Create a formatter and add it to the file handler
    file_formatter = logging.Formatter("%(asctime)s - %(name)s - %(levelname)s - %(message)s")
    file_handler.setFormatter(file_formatter)

    # Add the handlers to the logger
    logger.addHandler(file_handler)
    logger.addHandler(console_handler)

    return logger


# Set up loggers for different modules
app_logger = setup_logger("my-app", "my-app.log", logging.INFO)

```

Y﻿ou can make a Replace find with my-app and replace it for your actual app name.

T﻿his script colors the logs by category, stores it in the main dir logs directory (consistent with the dir scheme presented) and lets you add them into any method you like. 

A﻿n example of integration could be as follows:

```python
from myapp.logs.logger import app_logger

class DemoClass:
  def __init__(self):
    self.firstvar = "hello"
    app_logger.info("DemoClass initiated")
  
  def do_something(self):
    try:
      secondvar = self.firstbar + " again"
      app_logger.info("Secondvar set")
    except Exception as e:
      app_logger.error(f"Error in setting secondvar: {e})
      raise
```

B﻿y using this formula you are logging the methods and also catching possible errors with descriptive messages.