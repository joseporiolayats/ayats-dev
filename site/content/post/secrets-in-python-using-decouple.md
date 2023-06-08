---
title: "Secrets in Python: using Decouple"
date: 2023-06-08T10:49:11.776Z
description: Handling secrets in any app is challenging and critical, let's
  explore how to do it easily with Decouple
---
First of all you have to configure the .gitignore file just in case for excluding the secrets file .env

```shell
echo ".env" >> .gitignore
```

N﻿ow that we're sure your secrets won't get commited to your version control system, like git or github, we can proceed with creating the actual secrets file.

```shell
touch .env
```

W﻿e will be using .env file since it's the standard for handling secrets that are held as environment variables in the server machine.

T﻿hen we install the python secrets handler of our choice. A famous one is `python-dotenv` , but I prefer `decouple` for its simplicity and enhanced security.

```shell
poetry add decouple
```

T﻿hen in our .env file we list the secrets as follows

```toml
API_URL=http://myapis.com/myaddress
API_SECRET=supersecretkey
DB_URL=http://localhost:27017
DB_USER=my-username
DB_PASSWORD=supersecretpassword
```



A﻿nd inside our python script we can use those secrets without ever revealing them by importing decouple and configuring each variable as a lazy pointer to the .env entry.

```python
from decouple import config

api_url = config("API_URL")
api_secret = config("API_SECRET")
db_url = config("DB_URL")
db_user = config("DB_USER")
db_password = config("DB_PASSWORD")

# mongodb uri
```



N﻿ow we can make calls to those variables and compose new ones, like this example for a MongoDB uri

```python
uri = f'mongodb://{db_user}:{db_password}@{db_url}'

client = AsyncIOMotorClient(uri)
```



A﻿nd this is a fully secure system as long as our .env file stays safe.