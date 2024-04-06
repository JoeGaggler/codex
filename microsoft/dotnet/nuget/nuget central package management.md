`Directory.Packages.props`:
```xml
<Project>
  <PropertyGroup>
    <ManagePackageVersionsCentrally>true</ManagePackageVersionsCentrally>
    <CentralPackageTransitivePinningEnabled>true</CentralPackageTransitivePinningEnabled>
  </PropertyGroup>
</Project>
```

>[!NOTE]
> the file name is case-sensitive. 
> when the case is incorrect, `dotnet restore` will fail to correlate the package lock file with central package management
