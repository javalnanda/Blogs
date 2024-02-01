---
title: "Preventing Code Execution While Running Tests from CLI for Swift Package"
seoTitle: "Preventing production code execution while running tests"
seoDescription: "Check if tests are running when executing tests from command line for a swift package"
datePublished: Tue Jan 30 2024 09:14:20 GMT+0000 (Coordinated Universal Time)
cuid: cls056nxk000109ku6ijmcfa6
slug: preventing-code-execution-while-running-tests-from-cli-for-swift-package
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706605913644/9dcb9d3a-2a55-4005-9050-013837e5c116.png
tags: swift, ios, testing, swift-package-manager

---

Ideally, you would not require conditional logic in your production code to check if tests are running or the main app target is running. But, there are situations where you can't get around it in case of Integration tests or UI Tests.

There are various solutions which you might have come across such as:

```swift
var isRunningTests: Bool {
    return ProcessInfo.processInfo.environment["XCTestConfigurationFilePath"] != nil
}

// Usage
if isRunningTests {
} else {
}
```

Or setting your own environment variable for the test scheme/configuration and check it as below:

```swift
var isRunningTests: Bool {
    ProcessInfo.processInfo.environment["isRunningTest"] != nil 
}
```

While these solutions work fine for unit tests when running tests from Xcode (⌘+ U), it does not work when running tests from command line for a swift package using following command: `swift test`

### Solution:

While running tests from the command line, the name of the process that is getting executed is `xctest` . So, we can check if the current process is running tests as follows:

```swift
var isRunningTests: Bool {
    ProcessInfo.processInfo.processName == "xctest"
}
```

Let me know if you found this helpful. Feel free to tweet me on [Twitter](https://twitter.com/javalnanda) if you have any additional tips or feedback.

Thanks