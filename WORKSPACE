
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")


# Add rules_android so RJE's WORKSPACE graph can load its Starlark correctly.
# Version: v0.6.5 — tarball URL & SHA from the official release page.
http_archive(
    name = "rules_android",
    sha256 = "5a5182c74828da53165221987395264d4a5cee8c10c17178a0d5e123bbd1623c",
    strip_prefix = "rules_android-0.6.5",
    url = "https://github.com/bazelbuild/rules_android/releases/download/v0.6.5/rules_android-v0.6.5.tar.gz",
)


# --- rules_java 9.6.1 (pinned) + prerequisites ---
http_archive(
    name = "rules_java",
    urls = ["https://github.com/bazelbuild/rules_java/releases/download/9.6.1/rules_java-9.6.1.tar.gz"],
    sha256 = "9de4e178c2c4f98d32aafe5194c3f2b717ae10405caa11bdcb460ac2a6f61516",
)

http_archive(
    name = "bazel_features",
    url = "https://github.com/bazel-contrib/bazel_features/releases/download/v1.30.0/bazel_features-v1.30.0.tar.gz",
    strip_prefix = "bazel_features-1.30.0",
    sha256 = "a660027f5a87f13224ab54b8dc6e191693c554f2692fcca46e8e29ee7dabc43b",
)

load("@bazel_features//:deps.bzl", "bazel_features_deps")
bazel_features_deps()

load("@rules_java//java:rules_java_deps.bzl", "rules_java_dependencies")
rules_java_dependencies()

load("@com_google_protobuf//bazel/private:proto_bazel_features.bzl", "proto_bazel_features")  # buildifier: disable=bzl-visibility
proto_bazel_features(name = "proto_bazel_features")

load("@rules_java//java:repositories.bzl", "rules_java_toolchains")
rules_java_toolchains()
# --- end rules_java setup ---

# --- rules_jvm_external 6.10 (pinned) ---
RULES_JVM_EXTERNAL_TAG = "6.10"
RULES_JVM_EXTERNAL_SHA = "e5f83b8f2678d2b26441e5eafefb1b061826608417b8d24e5e8e15e585eab1ba"

http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    urls = [
        "https://github.com/bazel-contrib/rules_jvm_external/releases/download/%s/rules_jvm_external-%s.tar.gz"
        % (RULES_JVM_EXTERNAL_TAG, RULES_JVM_EXTERNAL_TAG),
    ],
)


load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")
rules_jvm_external_deps()


load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = [
        "org.seleniumhq.selenium:selenium-java:4.40.0",
        "org.testng:testng:7.10.2",
    ],
    repositories = [
        "https://repo1.maven.org/maven2",
    ],
    # After pinning, uncomment the next line:
    # maven_install_json = "//:maven_install.json",
)
