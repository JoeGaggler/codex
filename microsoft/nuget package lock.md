
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

if using azure devops:
```yaml
- task: DotNetCoreCLI@2
  inputs:
    command: 'restore'
    restoreArguments: '--locked-mode'
    verbosityRestore: 'Normal'
```
test