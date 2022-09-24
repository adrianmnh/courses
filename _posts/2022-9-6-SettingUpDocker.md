---
title: CSCI 381 - Data Modeling and Advanced Systems 2
author: adrian
date: 2022-9-6 09:02:00 -400
categories: [Databases]
tags: [docker]
pin: false
math: true
mermaid: true
image:
  path: /dm/logo.png
  width: 800
  height: 500
  alt: 
---

varchar in SQLServer


free 24GB oracle!!

```
file path for docker volumes

\\wsl.localhost\docker-desktop-data\data\docker\volumes

```



# MSSQL

```sql
my image -> 

docker container run --name testtest -p 20005:1433 -e "ACCEPT_EULA=Y" -e "MSSQL_AGENT_ENABLED=true" -e "SA_PASSWORD=legion$%^" -e "MSSQL_DATA_DIR=/var/opt/mssql/data/" -e "MSSQL_LOG_DIR=/var/opt/mssql/log/" -e "MSSQL_BACKUP_DIR=/var/opt/mssql/backup/" -v //zvol/test:/var/opt/mssql/backup -h microsoftSQLServer -d adriannoa91/sampledb:sqlserver


docker pull mcr.microsoft.com/mssql/server:2019-latest

docker container run --name MSSQLServer -p 20003:1433 -e "ACCEPT_EULA=Y" -e "MSSQL_AGENT_ENABLED=true" -e "SA_PASSWORD=legion$%^" -e "MSSQL_DATA_DIR=/var/opt/mssql/data/" -e "MSSQL_LOG_DIR=/var/opt/mssql/log/" -e "MSSQL_BACKUP_DIR=/var/opt/mssql/backup/" -v //zvol/sqlserver:/var/opt/mssql/backup -h microsoftSQLServer -d mcr.microsoft.com/mssql/server:2019-latest

docker exec -ti -u 0 MSSQLServer bash

cd /var/opt/mssql/backup

chmod -R 777 /var/opt/mssql

/opt/mssql-tools/bin/sqlcmd -U sa

RESTORE FILELISTONLY FROM DISK=N'/var/opt/mssql/backup/AdventureWorks2014.bak'
GO  

output

AdventureWorks2014_Data - AdventureWorks2014_Data.mdf
AdventureWorks2014_Log - AdventureWorks2014_Log.ldf

RESTORE DATABASE AdventureWorks2014 FROM DISK=N'/var/opt/mssql/backup/AdventureWorks2014.bak' WITH 
MOVE 'AdventureWorks2014_Data' to '/var/opt/mssql/data/AdventureWorks2014.mdf', 
MOVE 'AdventureWorks2014_Log' to '/var/opt/mssql/data/AdventureWorks2014_log.ldf'
GO


move 'Northwinds2019TSQLV5_log' to '/var/opt/mssql/data/northwinds2019.ldf'

SELECT
  *
FROM
  INFORMATION_SCHEMA.TABLES
WHERE
  TABLE_TYPE = 'BASE TABLE';
GO



CREATE DATABASE TestDB ON (FILENAME = 'C:\MySQLServer\TestDB_Data.mdf'), (FILENAME = 'C:\MySQLServer\ TestDB_Log.ldf') FOR ATTACH; 
```

# PostgreSQL

```sql

docker run --name PostgreSQL -p 20002:5432 -e POSTGRES_PASSWORD=legion$%^ -e PGDATA=/var/lib/postgresql/data/ -v //zvol/postgresql:/var/lib/postgresql/backup -d postgres:11.15-alpine3.15 


docker exec -ti -u 0 PostgreSQL bash                      

chmod -R 777 /var/lib/postgresql/backup/

psql -U postgres 
\l - list database
\c - choose database
\dt - show tables

psql -U postgres -d dvdrental < /var/lib/postgresql/backup/dvdrental/restore.sql;

psql -U postgres -d sportsdb < /var/lib/postgresql/backup/sportsdb.sql;

****** untested

sudo -u postgres pg_dump -Fc mydb > ./mydb.sql
sudo -u postgres dropdb mydb
sudo -u postgres createdb -O db_user mydb
sudo -u postgres pg_restore -d mydb < ./mydb.sql


```

# MySQL

```sql
docker run -d --name MySQL -h MySQLServer -p 20001:3306 -e MYSQL_ROOT_PASSWORD=legion$%^ -v //zvol/mysql:/var/lib/mysql-files/ -d mysql:latest

chmod -R 777 /var/lib/mysql

chmod -R 777 /var/lib/mysql-files

docker exec -it -u 0 MySQL bash

mysql -uroot -p 

## From mysql-files folder

mysql -uroot -p sakila < sakila-schema.sql
mysql -uroot -p sakila < sakila-data.sql

# from root

mysql -uroot -p sakila < /var/lib/mysql-files/sakila-schema.sql
mysql -uroot -p sakila < /var/lib/mysql-files/sakila-data.sql

```





