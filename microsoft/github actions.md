# terminology
workflow - equivalent to pipeline in ADO
# schema
## meta
`name:` - title of the run

## triggers
```yaml
on:
  push:
    branches: [ ]
  pull_request:
    branches: [ ] # target branch
  workflow_dispatch: # empty, allows manual runs
```

## jobs
`jobs:` , children have name of job instead of `job:` like ADO

## job
```yaml
myjob:
  runs-on: ubuntu-latest # or '[self-hosted, macOS]' for ANDed labels
  steps: [ ] # step
```

## step
```yaml
# invoke shared action
- uses: actions/checkout@v3

# run some script
- name: some title here
  shell: bash # default, or pwsh
  env:
    SOMEVAR: blah
  run: |
    echo some script
```

# notes
changing the `name` renames the workflow in GitHub
changing the file name sets up a different workflow, even if the `name` is the same

cleanup steps are done by adding `if: #{{ always() }}` to step

values in `env:` do not allow recursive expansion. workaround by appending to special location inside step:
```yaml
- name: env set
  run: |
    echo "MY_PATH=${GITHUB_WORKSPACE}/my_file" >> $GITHUB_ENV
```

## calling workflows
similar to `template` in Azure Pipelines, except more like a function call than macro expansion

a job that calls a workflow cannot have an `environment`, only jobs that have steps

call depth is limited to `2`, in effect you can have `stages` and `jobs` like in Azure Pipelines

in the ui, the name of the job consists of the caller and callee: `caller_name / callee_name`

