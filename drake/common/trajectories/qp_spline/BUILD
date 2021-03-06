# -*- python -*-
# This file contains rules for Bazel; see drake/doc/bazel.rst.

load("//tools:cpplint.bzl", "cpplint")
load("//tools:drake.bzl", "drake_cc_googletest", "drake_cc_library")

package(default_visibility = ["//visibility:public"])

drake_cc_library(
    name = "continuity_constraint",
    srcs = ["continuity_constraint.cc"],
    hdrs = ["continuity_constraint.h"],
    linkstatic = 1,
    deps = [
        "//drake/common",
    ],
)

drake_cc_library(
    name = "spline_generation",
    srcs = ["spline_generation.cc"],
    hdrs = ["spline_generation.h"],
    linkstatic = 1,
    deps = [
        ":spline_information",
        "//drake/common/trajectories:piecewise_polynomial",
    ],
)

drake_cc_library(
    name = "spline_information",
    srcs = ["spline_information.cc"],
    hdrs = ["spline_information.h"],
    linkstatic = 1,
    deps = [
        ":continuity_constraint",
        ":value_constraint",
        "//drake/common/trajectories:piecewise_polynomial",
    ],
)

drake_cc_library(
    name = "value_constraint",
    srcs = ["value_constraint.cc"],
    hdrs = ["value_constraint.h"],
    linkstatic = 1,
    deps = [
        "//drake/common",
    ],
)

# === test/ ===

drake_cc_googletest(
    name = "spline_generation_test",
    deps = [
        ":spline_generation",
    ],
)

cpplint()
