# openIMIS dockerized database

| :bomb: Disclaimer : NOT FOR PRODUCTION USE :bomb: |
| --- |
| This repository provides a dockerized openIMIS database. It provides a quick setup for development, testing or demoing. ***It is NOT INTENDED FOR PRODUCTION USE.*** |

Please look for the directions on the openIMIS Wiki: https://openimis.atlassian.net/wiki/spaces/OP/pages/963182705/MO1.1+Install+the+modular+openIMIS+using+Docker

Using the provided docker file, you can build a docker image running a SQL Server 2017, with a restored openIMIS backup database.
This is done by giving the following ARGs to the docker build command:
```
docker build \
  --build-arg ACCEPT_EULA=Y \
  --build-arg SA_PASSWORD=<your secret password> \
  --build-arg SQL_SCRIPT_URL=<url to the sql script to create the database> \
  . \
  -t openimis-db
```
***Notes***:
* by setting the ACCEPT_EULA=Y, you explicitely accept [Microsoft EULA](https://go.microsoft.com/fwlink/?linkid=857698) for the dockerized SQL Server 2017. Please ensure you read it and use the provided software according to the terms of that license.
* choose a strong password (at least 8 chars,...)... or SQL Server will complain
* if you don't provide the SQL_SCRIPT_URL, the [reference empty](https://github.com/openimis/database_ms_sqlserver/raw/master/Empty%20databases/openIMIS_ONLINE.sql) backup will be used

To start the image in a docker container: `docker run -p 1433:1433 openimis-db`
To restore the backup inside the container:
* To spot the ID of the container: `docker container ls` (spot the row with openimis-db IMAGE name)
* Launch the restore script: `docker exec <CONTAINER ID> /create_database.sh`

***Note:***
The database is writen within the container. If you want to keep your data between container execution, stop/start the container via `docker stop <CONTAINER ID>` / `docker start <CONTAINER ID>` (using `docker run ... ` recreates a new container from the image... thus without any data)
