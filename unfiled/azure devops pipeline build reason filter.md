skipping deployments for pull requests:
```yaml
- ${{ if ne(variables['Build.Reason'], 'PullRequest') }}:
```
