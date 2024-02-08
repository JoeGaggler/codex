# build number

default pipeline number:  `$(Build.DefinitionName)_$(Date:yyyyMMdd)$(Rev:.r)`

## with build reason

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

## with variables

```yaml
variables:
  - name: buildDate
    value: $[format('{0:yyyy}{0:MMdd}', pipeline.startTime)]
  - name: buildRevision
    value: $[counter(variables.buildDate, 0)]
  - name: buildVersion
    value: $[format('{0}_{1}_{2}', variables['Build.DefinitionName'], variables.buildDate, variables.buildRevision)]

name: '$(buildVersion)'
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

# force failure for skipped stage
work around for the issue that a timed-out approval is a skip instead of reject
```yaml
  - stage: checks
    condition: not(or(canceled(), failed())) # only check viable runs
    dependsOn:
      - previous_stage # the stage you care about
    jobs:
      - job: my_check
        condition: in(stageDependencies.previous_stage.somejob.result, 'Skipped')
        steps:
          - checkout: none
          - bash: |
              echo "##vso[task.logissue type=error]A critical stage was skipped."
              echo "##vso[task.complete result=Failed;]"
```
