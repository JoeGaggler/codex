instructions in additional to the basic setup from Microsoft.

# remove quarantine

remove "quarantine" from the downloaded zip file, otherwise builds will fail:
```bash
xattr -d com.apple.quarantine agent.zip
```

# recommended

install components from homebrew:
```sh
brew install cocoapods
brew install fastlane
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
