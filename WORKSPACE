load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "aspect_rules_js",
    sha256 = "c3b5fd40ec19f3260094321380169abe86dd89e3506c4e44a515a50c1626629b",
    strip_prefix = "rules_js-1.6.6",
    url = "https://github.com/aspect-build/rules_js/archive/refs/tags/v1.6.6.tar.gz",
)

http_archive(
    name = "aspect_rules_ts",
    sha256 = "1ed2dc702b3d5fcf2b8e6ca4a5dae23fbc8e5570643d2a5cf8f5f09c7c44bc15",
    strip_prefix = "rules_ts-1.0.0-rc6",
    url = "https://github.com/aspect-build/rules_ts/archive/refs/tags/v1.0.0-rc6.tar.gz",
)

http_archive(
    name = "aspect_rules_esbuild",
    sha256 = "dccab34d457faf9968ec83e2900d65cf5b846f036822b675d988deee0113dba9",
    strip_prefix = "rules_esbuild-0.13.1",
    url = "https://github.com/aspect-build/rules_esbuild/archive/refs/tags/v0.13.1.tar.gz",
)

http_archive(
    name = "aspect_bazel_lib",
    sha256 = "88ac1874c9930c5f01482d25a4f25104a788a178bf1c20053c00322ea7059bd6",
    strip_prefix = "bazel-lib-1.16.0",
    url = "https://github.com/aspect-build/bazel-lib/archive/refs/tags/v1.16.0.tar.gz",
)

load("@aspect_bazel_lib//lib:repositories.bzl", "aspect_bazel_lib_dependencies")

aspect_bazel_lib_dependencies()

##################
# rules_js setup #
##################

load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_js_dependencies()

load("@rules_nodejs//nodejs:repositories.bzl", "DEFAULT_NODE_VERSION", "nodejs_register_toolchains")

nodejs_register_toolchains(
    name = "nodejs",
    node_version = DEFAULT_NODE_VERSION,
)

load("@aspect_rules_js//npm:npm_import.bzl", "npm_translate_lock")

npm_translate_lock(
    name = "npm",
    # See bazel/examples/react/README.md for why we do not put the lock file in bazel/workspace
    pnpm_lock = "//:pnpm-lock.yaml",
    verify_node_modules_ignored = "//:.bazelignore",
)

load("@npm//:repositories.bzl", "npm_repositories")

npm_repositories()

##################
# rules_ts setup #
##################

# Fetches the rules_ts dependencies.
# If you want to have a different version of some dependency,
# you should fetch it *before* calling this.
# Alternatively, you can skip calling this function, so long as you've
# already fetched all the dependencies.
load("@aspect_rules_ts//ts:repositories.bzl", "rules_ts_dependencies", ts_latest_version = "LATEST_VERSION")

rules_ts_dependencies(ts_version = ts_latest_version)

#######################
# rules_esbuild setup #
#######################

# Fetches the rules_esbuild dependencies.
# If you want to have a different version of some dependency,
# you should fetch it *before* calling this.
# Alternatively, you can skip calling this function, so long as you've
# already fetched all the dependencies.
load("@aspect_rules_esbuild//esbuild:dependencies.bzl", "rules_esbuild_dependencies")

rules_esbuild_dependencies()

# Register a toolchain containing esbuild npm package and native bindings
load("@aspect_rules_esbuild//esbuild:repositories.bzl", "esbuild_register_toolchains", esbuild_latest_version = "LATEST_VERSION")

esbuild_register_toolchains(
    name = "esbuild",
    esbuild_version = esbuild_latest_version,
)
