typical git setup on a computer

# config commands

```bash
git config --global push.autoSetupRemote true
```

## global ignore
```bash
git config --global core.excludesfile ~/.gitignore_global
```

contents of `~/.gitignore_global`:
```
.DS_Store
```

# signing

## create key
[[generate a new ssh key]]

## setup allowed signers
```bash

touch ~/.ssh/allowed_signers
cat ~/.ssh/id_rsa.pub | pbcopy
code ~/.ssh/allowed_signers

# Add this line, fix order as shown:
# joegaggler@gmail.com ssh-rsa <PASTE_FROM_CLIPBOARD>

git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
```
