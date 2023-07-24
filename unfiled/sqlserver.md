docker

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=SQLServerIs#1" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2022-latest
```

procgen connection string
```json
"Connection String": "Server=localhost;Database=DATABASE;User ID=sa;Password=SQLServerIs#1;Encrypt=false;"
```
