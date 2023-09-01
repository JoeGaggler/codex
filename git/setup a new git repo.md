typical setup for a git repo

# global
verify global config first: [[setup git global config]]

# init
```bash
git init
git config user.name "Me"
git config user.email "me@gmail.com"
git remote add origin git@github.com:JoeGaggler/codex.git
```

# signing
if not already setup in [[setup git global config|global configuration]]: 
```bash
git config user.signingkey ~/.ssh/id_ed25519.pub
git config commit.gpgsign true
git config gpg.format ssh
git config gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
```

verify first commit signature before push to remote:
```bash
git log --show-signature
```
