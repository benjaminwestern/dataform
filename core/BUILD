load("//:version.bzl", "DF_VERSION")
load("//testing:index.bzl", "ts_test_suite")
load("//tools:expand_template.bzl", "expand_template")
load("//tools:node_modules.bzl", "node_modules")
load("//tools:ts_library.bzl", "ts_library")

package(default_visibility = ["//visibility:public"])

expand_template(
    name = "version",
    out = "version.ts",
    substitutions = {
        "$DF_VERSION": DF_VERSION,
    },
    template = "version.ts.tmpl",
)

ts_library(
    name = "core",
    srcs = [
        "actions/assertion.ts",
        "actions/data_preparation.ts",
        "actions/declaration.ts",
        "actions/incremental_table.ts",
        "actions/index.ts",
        "actions/notebook.ts",
        "actions/operation.ts",
        "actions/table.ts",
        "actions/test.ts",
        "actions/view.ts",
        "column_descriptors.ts",
        "compilers.ts",
        "contextables.ts",
        "index.ts",
        "main.ts",
        "path.ts",
        "session.ts",
        "targets.ts",
        "utils.ts",
        "workflow_settings.ts",
        ":version.ts",
    ],
    deps = [
        "//common/errors",
        "//common/protos",
        "//common/strings",
        "//core/compilation_sql",
        "//protos:ts",
        "//sqlx:lexer",
        "@npm//@types/fs-extra",
        "@npm//@types/js-yaml",
        "@npm//@types/node",
        "@npm//@types/semver",
        "@npm//fs-extra",
        "@npm//js-yaml",
        "@npm//protobufjs",
        "@npm//semver",
        "@npm//tarjan-graph",
    ],
)

ts_test_suite(
    name = "tests",
    srcs = [
        "main_test.ts",
        "actions/assertion_test.ts",
        "actions/data_preparation_test.ts",
        "actions/declaration_test.ts",
        "actions/incremental_table_test.ts",
        "actions/index_test.ts",
        "actions/notebook_test.ts",
        "actions/operation_test.ts",
        "actions/table_test.ts",
        "actions/test_test.ts",
        "actions/view_test.ts",
    ],
    data = [
        ":node_modules",
    ],
    deps = [
        ":core",
        "//common/protos",
        "//protos:ts",
        "//testing",
        "//testing:run_core",
        "@npm//@types/chai",
        "@npm//@types/fs-extra",
        "@npm//@types/js-yaml",
        "@npm//@types/node",
        "@npm//chai",
        "@npm//fs-extra",
        "@npm//js-yaml",
    ],
)

node_modules(
    name = "node_modules",
    deps = [
        "//packages/@dataform/core:package_tar",
    ],
)
