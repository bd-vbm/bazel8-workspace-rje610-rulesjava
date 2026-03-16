
# Bazel 8.5 WORKSPACE starter with rules_java 9.6.1 and rules_jvm_external 6.10

## Pin Maven deps
```bash
bazel run @maven//:pin --config=workspace
# then edit WORKSPACE and set: maven_install_json = "//:maven_install.json"
```

## Build (WORKSPACE)
```bash
bazel build //java_app:app //cpp_app:hello --config=workspace
bazel test  //java_app:app_testng --config=workspace
```
