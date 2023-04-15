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
