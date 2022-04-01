dotnet tool install needs `--verbosity minimal` to prompt for device login.

dotnet restore does not pick up packages that are recently pushed to the feed. use this command to reset the local cache: `dotnet nuget locals all --clear`

`Microsoft.Data.SqlClient` requires `Encrypt=false` in connection string for local connections, or ones without a certificate.
