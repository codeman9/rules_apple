load("@bazel_skylib//rules:build_test.bzl", "build_test")
load(
    "@build_bazel_rules_swift//swift:swift.bzl",
    "swift_library",
)
load("//apple:visionos.bzl", "visionos_application")
load("//apple:versioning.bzl", "apple_bundle_version")

licenses(["notice"])

swift_library(
    name = "Sources",
    srcs = [
        "Sources/ContentView.swift",
        "Sources/HelloWorldApp.swift",
    ],
)

apple_bundle_version(
    name = "HelloWorldVersion",
    build_version = "1.0",
    short_version_string = "1.0",
)

visionos_application(
    name = "HelloWorld",
    app_icons = ["//examples/resources:VisionAppIcon.xcassets"],
    bundle_id = "com.example.hello-world",
    infoplists = [":Info.plist"],
    minimum_os_version = "1.0",
    target_compatible_with = select({
        "//:supports_visionos_setting": [],
        "//conditions:default": ["@platforms//:incompatible"],
    }),
    version = ":HelloWorldVersion",
    deps = [":Sources"],
)

build_test(
    name = "HelloWorldBuildTest",
    target_compatible_with = select({
        "//:supports_visionos_setting": [],
        "//conditions:default": ["@platforms//:incompatible"],
    }),
    targets = [
        ":HelloWorld",
    ],
)
