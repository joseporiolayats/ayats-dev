---
title: How to start ArangoDB with Docker
date: 2023-06-06T16:26:21.540Z
description: How to get ArangoDB up and running
---
# S﻿tart a Server

S﻿tart with docker run

```shell
sudo docker run -e ARANGO_RANDOM_ROOT_PASSWORD=1 -p 8529:8529 -d --name arangodb-instance arangodb
```

T﻿he root password will be automatically generated. In order to discover it you have to check the docker logs.

```shell
sudo docker logs arangodb-instance
```

B﻿ut this method gets cumbersome and the password, which will appear at the beginning of the logs, can be hard to copy. So use instead this command in order to retrieve it from the logs and store it directly to a `.env file`.

```shell
echo "DB_PASSWORD=$(sudo docker logs arangodb-instance | sed -n 's/.*GENERATED ROOT PASSWORD: \(.*\)$/\1/p')" > .env
```

N﻿ow you have the password, which you don't know, stored in a .env file which you can copy into the root of your working directory, which you can check by entering the .env file or by typing

```shell
cat .env
```

You can check that the database is working properly by accessing it at http://localhost:8529 using the username root and the password from the .env file.