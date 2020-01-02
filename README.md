# Bazel test hosts for Apple targets

This repository provides a generic Apple test host that can be used when testing Apple targets with
[Bazel](http://bazel.build/).

## Example

First, define the repository in your `WORKSPACE`:

```
git_repository(
    name = "bazel_test_host_apple",
    remote = "https://github.com/material-foundation/bazel-test-host-apple.git",
    commit = "<#a sha for this repo#>",
)
```

You can then use the provided test host, `@bazel_test_host_apple//test_host` in your testing targets
like so:

```
load("@build_bazel_rules_apple//apple:ios.bzl", "ios_ui_test_suite")
load("@build_bazel_rules_apple//apple/testing/default_runner:ios_test_runner.bzl", "ios_test_runner")

objc_library(
    name = "UITestsLib",
    testonly = 1,
    srcs = ["UITests.m"],
)	

ios_test_runner(
    name = "IPHONE_7_PLUS_IN_10_3",
    device_type = "iPhone 7 Plus",
    os_version = "10.3",
)

ios_test_runner(
    name = "IPHONE_X_IN_11_4",
    device_type = "iPhone X",
    os_version = "11.4",
)

ios_test_runner(
    name = "IPHONE_XS_MAX_IN_12_2",
    device_type = "iPhone Xs Max",
    os_version = "12.2",
)

ios_ui_test_suite(
    name = "UITests",
    deps = [
      ":UITestsLib",
    ],
    test_host = "@bazel_test_host_apple//test_host",
    minimum_os_version = "9.0",
    timeout = "moderate",
    flaky = 1,
    runners = [
        ":IPHONE_7_PLUS_IN_10_3",
        ":IPHONE_X_IN_11_4",
        ":IPHONE_XS_MAX_IN_12_2",
    ],
)
```

## License

Licensed under the Apache 2.0 license. See LICENSE for details.
