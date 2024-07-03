instructions in additional to the basic setup from Microsoft.

# remove quarantine

remove "quarantine" from the downloaded zip file, otherwise builds will fail:
```bash
xattr -d com.apple.quarantine agent.zip
```

# recommended

install components from homebrew:
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install jq
brew install dotnet
brew install dotnet@6
brew install cocoapods
brew install fastlane
brew install libressl
echo 'export PATH="/opt/homebrew/opt/libressl/bin:$PATH"' >> ~/.zshrc
brew install --cask visual-studio-code
brew install java
echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc
brew install powershell/tap/powershell
brew install --cask docker
brew install azure-cli
```

# preventing machine from sleeping
Edit the `runsvc.sh` file, insert the `caffeinate` command as shown below after obtaining the `PID`:
```bash
# run the host process which keep the listener alive
./externals/node16/bin/node ./bin/AgentService.js &
PID=$!
/usr/bin/caffeinate -ims -w ${PID}
wait $PID
```

# add agent capabilities
```sh
# pwd in agent root
echo "fastlane=1" >> .env
echo "docker=1" >> .env
echo "dotnet8=1" >> .env
```
