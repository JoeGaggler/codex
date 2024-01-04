add property to csproj:
```xml
<PropertyGroup>
  <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
</PropertyGroup>
```

restore:
```bash
dotnet restore --locked-mode
```
