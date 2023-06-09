testing framework for [[Xcode]]

# tricks

pass values to the test when running `xcbuild` by adding the prefix `TEST_RUNNER_` to your environment variable names. 

from a `XCTestCase`: read the environment variables (without `TEST_RUNNER_`) via `ProcessInfo.processInfo.environment`, then forward to the iOS app by appending to `app.launchArguments`.

```swift
// bash:
// TEST_RUNNER_UITestRegionCode=RDB xcodebuild test-without-building ...

let regionCode = ProcessInfo.processInfo.environment["UITestRegionCode"]

let app = XCUIApplication()
app.launchArguments.append("-UITestRegionCode")
app.launchArguments.append(regionCode)
```
