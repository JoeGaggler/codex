https://hub.docker.com/_/microsoft-mssql-server
https://learn.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-ver16&pivots=cs1-bash

```
docker run --name localdb -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=SqlServerIs#1" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2022-latest
```

on apple silicon:
```
docker run --name localdb --platform=linux/amd64 -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=SqlServerIs#1" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2022-latest
``````
