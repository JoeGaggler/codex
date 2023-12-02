```yaml
variables:
  - name: majorMinor
    value: $[format('{0:yy}.{0:Mdd}', pipeline.startTime)]
  - name: revisionCounter
    value: $[counter(variables.majorMinor, 0)]
  - name: version
    value: $[format('{0}.{1}', variables.majorMinor, variables.revisionCounter)]

name: '$(BuildDefinitionName)-$(Build.SourceBranchName)-$(version)'
```