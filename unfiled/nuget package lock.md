
in csproj:
```xml
<PropertyGroup> 
  <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
</PropertyGroup>
```

in ci pipeline:
```
dotnet.exe restore --locked-mode
```
