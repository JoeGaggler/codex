remove `--dry-run` to perform delete:
```bash
`az acr run --registry registrynamehere --cmd 'acr purge --untagged --filter "reponamehere:.*" --ago 60d --keep 100 --dry-run' /dev/null`
```