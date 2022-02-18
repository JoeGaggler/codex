
[logging commands](https://docs.microsoft.com/en-us/azure/devops/pipelines/scripts/logging-commands)

log error in the timeline of the task
`##vso[task.logissue type=error]Something went very wrong.`

log error in the text output:
`##[error]Something went very wrong.`

set variable:
`##vso[task.setvariable variable=myvar;isoutput=true;issecret=false;]canned goods`

----

[yaml schema](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema/?view=azure-pipelines&viewFallbackFrom=azure-devops)

[pipeline resources](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/about-resources?view=azure-devops&tabs=yaml)

----

#todo - see if `convertToJson` works to convert complex yaml parameters to json strings

```powershell
$myconfig = '${{ convertToJson(parameters.config) }}' | ConvertFrom-Json -Depth 10
```
