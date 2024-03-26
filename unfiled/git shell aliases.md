```bash
# get up to date with remote branch
gitup() {
    git fetch
    git merge origin/$1
}

# get changes over here
gitover() {
    git fetch
    git merge --squash --no-commit origin/$1
}
```
