typical git setup on a computer

# config commands

```bash
git config --global push.autoSetupRemote true
```

# signing

## create key
#todo: creating an ssh key for git

## setup allowed signers
```bash

touch ~/.ssh/allowed_signers
cat ~/.ssh/id_rsa.pub | pbcopy
code ~/.ssh/id_rsa.pub

# Add this line:
# joegaggler@gmail.com ssh-rsa <PASTE_FROM_CLIPBOARD>

git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
```
