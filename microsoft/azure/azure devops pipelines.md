# build number

default pipeline number:  `$(Build.DefinitionName)_$(Date:yyyyMMdd)$(Rev:.r)`

```yaml
variables:
	${{ if eq(variables['Build.Reason'], 'PullRequest') }}:
	  triggerCode: p
	${{ elseif eq(variables['Build.Reason'], 'Manual' ) }}:
	  triggerCode: m
	${{ elseif eq(variables['Build.Reason'], 'IndividualCI' ) }}:
	  triggerCode: c
	${{ elseif eq(variables['Build.Reason'], 'BatchedCI' ) }}:
	  triggerCode: c
	${{ elseif eq(variables['Build.Reason'], 'Schedule' ) }}:
	  triggerCode: s
	${{ elseif eq(variables['Build.Reason'], 'ResourceTrigger' ) }}:
	  triggerCode: r
	${{ else }}:
	  triggerCode: ${{ variables['Build.Reason'] }}

name: $(TeamProject)_$(SourceBranchName)_$(triggerCode)_$(Date:yyyyMMdd)$(Rev:.r)
```

# access values across stages and jobs
[Official Documentation](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/expressions?view=azure-devops#job-to-job-dependencies-across-stages)

```yaml
- stage: one_stage
  jobs:
	- job: one_job
	  steps:
	    - bash: echo "##vso[task.setvariable variable=one_var;isOutput=true]HELLO!!!"
	      name: one_step

	- job: two_job
	  dependsOn: one_job # required for access to 'one_var'
	  variables:
		foo: $[ dependencies.one_job.outputs['one_step.one_var'] ] ### foo=HELLO!!!

- stage: two
  dependsOn: one_stage # required for access to 'one_var'
  jobs:
	- job:
	  variables:
		foo: $[ stageDependencies.one_stage.one_job.outputs['one_step.one_var'] ] ### foo=HELLO!!!
```
