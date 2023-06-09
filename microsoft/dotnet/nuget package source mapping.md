https://learn.microsoft.com/en-us/nuget/consume-packages/package-source-mapping

example `nuget.config`:
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <config>
    <add key="repositorypath" value=".\packages" />
  </config>
  <packageSources>
    <add key="My Packages" value="https://pkgs.dev.azure.com/Me/_packaging/Internal/nuget/v3/index.json" />
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
  </packageSources>
  <packageSourceMapping>
    <packageSource key="nuget.org">
      <package pattern="*" />
    </packageSource>
    <packageSource key="My Packages">
      <package pattern="Mine.*" />
    </packageSource>
  </packageSourceMapping>
</configuration>
```
