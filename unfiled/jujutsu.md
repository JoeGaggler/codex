https://steveklabnik.github.io/jujutsu-tutorial/

# existing repo
```sh
jj git init --colocate
jj config set --user user.name "Some One"
jj config set --user user.email "someone@example.com"
jj abandon
jj bookmark track main@origin
jj config set --user ui.default-command log
```

## repo settings
```toml
[git]
push-bookmark-prefix = "user/joe/jj-"
```
