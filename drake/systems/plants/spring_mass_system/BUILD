# -*- python -*-
# This file contains rules for Bazel; see drake/doc/bazel.rst.

load("//tools:cpplint.bzl", "cpplint")
load("//tools:drake.bzl", "drake_cc_googletest", "drake_cc_library")

package(default_visibility = ["//visibility:public"])

drake_cc_library(
    name = "spring_mass_system",
    srcs = ["spring_mass_system.cc"],
    hdrs = ["spring_mass_system.h"],
    linkstatic = 1,
    deps = [
        "//drake/systems/framework",
    ],
)

# === test/ ===

drake_cc_googletest(
    name = "spring_mass_system_test",
    deps = [
        ":spring_mass_system",
        "//drake/common:eigen_matrix_compare",
    ],
)

cpplint()
