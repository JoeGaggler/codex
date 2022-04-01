## repo setup
create manifest file in repo: `dotnet new tool-manifest`

install the tool: `dotnet tool install Emdat.DotNetCLI.GenSpec --add-source https://pkgs.dev.azure.com/Emdat/_packaging/DotNetCLI/nuget/v3/index.json --verbosity minimal --interactive`

## via visual studio
add yaml file to same directory: `.codegen.yml`

contents:
```yml
files:
- file: specification.genspec.txt
  tool: dotnet-genspec
  extension: cs

```


set custom tool on specification to either:
* DotNetCLIToolCsCodeGenerator
* Jmg.CodeGen

-----
## via shell
```bash
dotnet tool run dotnet-genspec --namespace MyNS --name specification.genspec.txt --extension .cs < input.txt > output.cs
```
