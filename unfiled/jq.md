print an array of name-value pairs
```bash
echo $json | jq -r '.[] | "\(.name) => \(.value)"'
echo $json | jq -r '.[] | "\(.name) => \(.value | @json)"'
echo $json | jq -r '.[] | "\(.name) => \(.value | @json | .[1:-1])"'
```
