# Copyright 2020-present The Material Foundation Authors. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")

git_repository(
    name = "build_bazel_rules_apple",
    remote = "https://github.com/bazelbuild/rules_apple.git",
    commit = "96212456d3cd7be9760fe28c077673bb85d46500",  # Dec 18, 2019
    shallow_since = "1576719323 -0800",  # Recommended by bazel.
)

git_repository(
    name = "build_bazel_rules_swift",
    remote = "https://github.com/bazelbuild/rules_swift.git",
    commit = "d7757c5ee9724df9454edefa3b4455a401a2ae22",  # Dec 19, 2019
    shallow_since = "1576775454 -0800",  # Recommended by bazel.
)

git_repository(
    name = "build_bazel_apple_support",
    remote = "https://github.com/bazelbuild/apple_support.git",
    commit = "9605c3da1c5bcdddc20d1704b52415a6f3a5f422",  # Oct 11, 2019
    shallow_since = "1570831694 -0700",  # Recommended by bazel.
)

load(
    "@build_bazel_rules_apple//apple:repositories.bzl",
    "apple_rules_dependencies",
)

apple_rules_dependencies()

load(
    "@build_bazel_rules_swift//swift:repositories.bzl",
    "swift_rules_dependencies",
)

swift_rules_dependencies()

load(
    "@build_bazel_apple_support//lib:repositories.bzl",
    "apple_support_dependencies",
)

apple_support_dependencies()

# This override of the zlib package resolves the following error:
# "no such package '@zlib//': The repository '@zlib' could not be resolved"
# Additional context available at: https://github.com/bazelbuild/bazel/issues/10270
http_archive(
    name = "zlib",
    build_file = "@com_google_protobuf//:third_party/zlib.BUILD",
    sha256 = "c3e5e9fdd5004dcb542feda5ee4f0ff0744628baf8ed2dd5d66f8ca1197cb1a1",
    strip_prefix = "zlib-1.2.11",
    urls = [
        "https://mirror.bazel.build/zlib.net/zlib-1.2.11.tar.gz",
        "https://zlib.net/zlib-1.2.11.tar.gz",
    ],
)

# This override resolves the following error:
# "error loading package '@com_google_protobuf//': Unable to find package for @rules_python//python:defs.bzl: The repository '@rules_python' could not be resolved"
http_archive(
    name = "rules_python",
    sha256 = "c911dc70f62f507f3a361cbc21d6e0d502b91254382255309bc60b7a0f48de28",
    strip_prefix = "rules_python-38f86fb55b698c51e8510c807489c9f4e047480e",
    urls = ["https://github.com/bazelbuild/rules_python/archive/38f86fb55b698c51e8510c807489c9f4e047480e.tar.gz"],
)
