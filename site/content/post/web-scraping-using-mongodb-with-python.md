---
title: Web Scraping using MongoDB with Python
date: 2023-06-06T20:39:44.461Z
description: Web Scraping using MongoDB in a docker container and Scrapy on python.
---
# Starting the database

U﻿sing docker, this command will look for the image of mongodb community on the latest version, and if it doesn't find it it will download and start.

A﻿lso, it will set the `root_username=user` so you have to change it, aswell as the `root_password=pass`

It will be listening to the default port 27017.

```shell
docker run --name mongodb -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=user -e MONGO_INITDB_ROOT_PASSWORD=pass mongodb/mongodb-community-server:latest
```

U﻿sing the async driver for mongodb in python `motor`:

```shell
poetry add motor
```

I﻿t will install all the dependencies.

# P﻿ython script

I﻿n python, we can create a script to interact with the database. We're going to make use of environment variables in order to setup the config. 

A﻿dd an execption in the `.gitignore` in order to not include the `.env` file! This is critical for security!.

F﻿irst create a `.env` file and put the data as follows:

```gitconfig
DB_URL=http://localhost:27017
DB_NAME=my_db
DB_USER=root
DB_PASSWORD=mypass
```

T﻿hen we'll use the python package `decouple` to preserve the secrets:

```
poetry add decouple
```

N﻿ext we create a python script for the actual database handling. 

T﻿he imports look like this:

```python
# my_app/database.py
"""
This module contains the database class.
"""
from decouple import config
from motor.motor_asyncio import AsyncIOMotorClient
from pymongo.errors import PyMongoError

from my_app.logs.logger import app_logger
```

T﻿hen we call the environment variables

```python
# read the connection string from the environment variables
db_url = config("DB_URL")
db_name = config("DB_NAME")
db_user = config("DB_USER")
db_pwd = config("DB_PASSWORD")
```

N﻿ext we create the database class:

```python
class MongoDBCRUD:
    """
    A class to handle CRUD operations for MongoDB.

    Attributes:
        client (AsyncIOMotorClient): An asynchronous MongoDB client.
        db (AsyncIOMotorDatabase): An asynchronous MongoDB database.
        collection (AsyncIOMotorCollection): An asynchronous MongoDB collection.
    """

    def __init__(self, collection_name: str):
        """
        Initializes MongoDBCRUD with the given collection name.

        Args:
            collection_name (str): The name of the collection to be used.
        """
        uri = f'mongodb://{db_user}:{db_pwd}@{db_url}'
        self.client = AsyncIOMotorClient(uri)
        self.db = self.client[db_name]
        self.collection = self.db[collection_name]
```

I﻿n this code block, the initializer passes the database object into the class with the properly authenticated driver client and with the selected collection.

T﻿he async operations need to be defined as in the enter and exit methods are necessary for all the synching after the work is done. Also we include a method to check that the server is readily available:

```python
# continuing the MongoDB_CRUD class
async def _initialize(self) -> None:
        """
        Initializes the MongoDBCRUD instance by checking if the MongoDB server
        is available.

        Returns:
            None
        """
        try:
            await self.client.admin.command("ismaster")
            app_logger.info("Connected to MongoDB server")
        except Exception as e:
            app_logger.error(f"Error initializing MongoDBCRUD: {e}")
            raise

    async def __aenter__(self):
        """
        Enters the asynchronous context manager.

        Returns:
            self (MongoDBCRUD): The current instance of MongoDBCRUD.
        """
        return self

    async def __aexit__(self, exc_type, exc_val, exc_tb) -> None:
        """
        Exits the asynchronous context manager and closes the MongoDB connection.

        Args:
            exc_type: The type of exception raised, if any.
            exc_val: The instance of exception raised, if any.
            exc_tb: The traceback object encapsulating the call stack, if any.

        Returns:
            None
        """
        await self.client.close()
        app_logger.info("Closed connection to MongoDB server")
```



A﻿nd finally the Create-Replace-Update-Delete CRUD operations, with finding:

```python
   @classmethod
    async def create_instance(cls, collection_name: str):
        """
        Creates an instance of MongoDBCRUD with the given collection name.

        Args:
            collection_name (str): The name of the collection to be used.

        Returns:
            instance (MongoDBCRUD): An instance of MongoDBCRUD.
        """
        instance = cls(collection_name)
        await instance._initialize()
        return instance
        
      async def insert_one(self, document: dict) -> str:
        """
        Inserts a single document into the collection.

        Args:
            document (dict): The document to be inserted.

        Returns:
            str: The ObjectId of the inserted document as a string.
        """
        try:
            result = await self.collection.insert_one(document)
            app_logger.info(f"Inserted document with ID: {str(result.inserted_id)}")
            return str(result.inserted_id)
        except Exception as e:
            app_logger.error(f"Error inserting document: {e}")
            raise

    async def find_one(self, query):
        """
        Find a single document in the collection based on a query.

        Args:
            query: The query to filter documents.

        Returns:
            The found document, if any.
        """
        try:
            result = await self.collection.find_one(query)
            if result:
                app_logger.info(f"Found document: {result}")
            else:
                app_logger.warning("Document not found")
            return result
        except PyMongoError as e:
            app_logger.error(f"Error finding document: {e}")

    async def update_one(self, query, update):
        """
        Update a single document in the collection based on a query.

        Args:
            query: The query to filter documents.
            update: The update to apply to the document.

        Returns:
            The number of modified documents.
        """
        try:
            result = await self.collection.update_one(query, update)
            app_logger.info(f"Updated {result.modified_count} document(s)")
            return result.modified_count
        except PyMongoError as e:
            app_logger.error(f"Error updating document: {e}")

    async def delete_one(self, query):
        """
        Delete a single document in the collection based on a query.

        Args:
            query: The query to filter documents.

        Returns:
            The number of deleted documents.
        """
        try:
            result = await self.collection.delete_one(query)
            app_logger.info(f"Deleted {result.deleted_count} document(s)")
            return result.deleted_count
        except PyMongoError as e:
            app_logger.error(f"Error deleting document: {e}")
```



N﻿ow we have all the building blocks to ensure a proper management of the database.