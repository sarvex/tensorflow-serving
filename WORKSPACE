workspace(name = "tf_serving")

# ===== TensorFlow dependency =====
#
# TensorFlow is imported here instead of in tf_serving_workspace() because
# existing automation scripts that bump the TF commit hash expect it here.
#
# To update TensorFlow to a new revision.
# 1. Update the 'git_commit' args below to include the new git hash.
# 2. Get the sha256 hash of the archive with a command such as...
#    curl -L https://github.com/tensorflow/tensorflow/archive/<git hash>.tar.gz | sha256sum
#    and update the 'sha256' arg with the result.
# 3. Request the new archive to be mirrored on mirror.bazel.build for more
#    reliable downloads.
load("//tensorflow_serving:repo.bzl", "tensorflow_http_archive")
tensorflow_http_archive(
    name = "org_tensorflow",
    sha256 = "c301bc909866e836f61e077244b2384055a6e64d827e8b964cc4ef7727468af0",
    git_commit = "3b4b5130e3b7eb7ed665394b1e56ddc507f817ce",
)

# Import all of TensorFlow Serving's external dependencies.
# Downstream projects (projects importing TensorFlow Serving) need to
# duplicate all code below in their WORKSPACE file in order to also initialize
# those external dependencies.
load("//tensorflow_serving:workspace.bzl", "tf_serving_workspace")
tf_serving_workspace()

# Check bazel version requirement, which is stricter than TensorFlow's.
load(
    "@org_tensorflow//tensorflow:version_check.bzl",
    "check_bazel_version_at_least"
)
check_bazel_version_at_least("3.7.2")

# Initialize TensorFlow's external dependencies.
load("@org_tensorflow//tensorflow:workspace3.bzl", "workspace")
workspace()
load("@org_tensorflow//tensorflow:workspace2.bzl", "workspace")
workspace()
load("@org_tensorflow//tensorflow:workspace1.bzl", "workspace")
workspace()
load("@org_tensorflow//tensorflow:workspace0.bzl", "workspace")
workspace()

# Initialize bazel package rules' external dependencies.
load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")
rules_pkg_dependencies()

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

rules_proto_dependencies()
rules_proto_toolchains()

