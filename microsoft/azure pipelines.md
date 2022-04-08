
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

https://docs.microsoft.com/en-us/azure/devops/pipelines/process/expressions?view=azure-devops#converttojson

```powershell
$myconfig = '${{ convertToJson(parameters.config) }}' | ConvertFrom-Json -Depth 10
```

-----

static variables are not available inside of a template invocation. you must pass these as parameters instead. source?

----

if you want to use static variables in the same scope, the `variables` section must appear before their usage.

example: trying to use a stage-variable to control a stage-displayName

----

when consuming a pipeline resource, you can access [variables from a triggering pipeline](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema/resources-pipelines-pipeline?view=azure-pipelines#the-pipeline-resource-metadata-as-predefined-variables) via runtime-variables:

```yaml
variables:
  MyVar: $[ variables['resources.pipeline.<ALIAS>.runID'] ]
```
