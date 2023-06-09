xcode simulator controller

# common commands
```bash
# list devices
xcrun simctl list devices

# with details in json format
xcrun simctl list devices --json

# boot up a simulator
xcrun simctl boot "iPhone 14 Pro"

# clone (useful isolated testing)
xcrun simctl clone "My iPhone" "com.apple.CoreSimulator.SimDeviceType.iPhone-14-Pro"

# uninstall an app
xcrun simctl uninstall "Smoke Test Device" "com.emdat.InSync"
```
