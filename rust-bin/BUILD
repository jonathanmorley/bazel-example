load("@crate_index//:defs.bzl", "aliases", "all_crate_deps")
load("@rules_rust//rust:defs.bzl", "rust_binary", "rust_clippy", "rust_library", "rust_test")
load("@vaticle_bazel_distribution//common/assemble_versioned:rules.bzl", "assemble_versioned")
load("@vaticle_bazel_distribution//github:rules.bzl", "deploy_github")
load("@rules_pkg//pkg:zip.bzl", "pkg_zip")

rust_library(
    name = "lib",
    crate_name = "rust_bin",
    srcs = glob(["src/**/*.rs"]),
    aliases = aliases(),
    deps = all_crate_deps(
        normal = True,
    ),
    proc_macro_deps = all_crate_deps(
        proc_macro = True,
    ),
)

rust_binary(
    name = "rust-bin",
    srcs = glob(["src/**/*.rs"]),
    aliases = aliases(),
    deps = [":lib"] + all_crate_deps(
        normal = True,
    ),
    proc_macro_deps = all_crate_deps(
        proc_macro = True,
    ),
)

rust_test(
    name = "test",
    crate = ':rust-bin',
    deps = all_crate_deps(
        normal_dev = True,
    ),
    proc_macro_deps = all_crate_deps(
        proc_macro_dev = True,
    ),
)

pkg_zip(
    name = "package",
    out = "rust-bin.zip",
    srcs = [":rust-bin"],
)

deploy_github(
  name = "publish",
  archive = ":package",
  organisation = "jonathanmorley",
  repository = "bazel-example"
)