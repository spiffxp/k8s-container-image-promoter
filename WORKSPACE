load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# You *must* import the Go rules before setting up the go_image rules.
http_archive(
    name = "io_bazel_rules_go",
    urls = ["https://github.com/bazelbuild/rules_go/releases/download/0.16.6/rules_go-0.16.6.tar.gz"],
    sha256 = "ade51a315fa17347e5c31201fdc55aa5ffb913377aa315dceb56ee9725e620ee",
)

http_archive(
    name = "bazel_gazelle",
    urls = ["https://github.com/bazelbuild/bazel-gazelle/releases/download/0.16.0/bazel-gazelle-0.16.0.tar.gz"],
    sha256 = "7949fc6cc17b5b191103e97481cf8889217263acf52e00b560683413af204fcb",
)

load("@io_bazel_rules_go//go:def.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains()

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

gazelle_dependencies()

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "aed1c249d4ec8f703edddf35cbe9dfaca0b5f5ea6e4cd9e83e99f3b0d1136c3d",
    strip_prefix = "rules_docker-0.7.0",
    urls = ["https://github.com/bazelbuild/rules_docker/archive/v0.7.0.tar.gz"],
)

load(
    "@io_bazel_rules_docker//go:image.bzl",
    _go_image_repos = "repositories",
)

_go_image_repos()

go_repository(
    name = "in_gopkg_yaml_v2",
    commit = "51d6538a90f86fe93ac480b35f37b2be17fef232",
    importpath = "gopkg.in/yaml.v2",
)

load("@io_bazel_rules_docker//container:container.bzl", "container_pull")

container_pull(
    name = "google-sdk-base",
    registry = "index.docker.io",
    repository = "google/cloud-sdk",
    # Version 234.0.0
    digest = "sha256:03ac1fb1715bb7a98163ffdc08bc66c57b555e7bfe03a904a9a1ef4be5bb2bd4",
)

# Maybe use cloud-builders/gcloud, for GCB. But for Prow just use the google-sdk
# one.
#container_pull(
#    name = "google-sdk-base",
#    registry = "gcr.io",
#    repository = "cloud-builders/gcloud",
#    # Version 232.0.0
#    digest = "sha256:6e6b1e2fd53cb94c4dc2af8381ef50bf4c7ac49bc5c728efda4ab15b41d0b510",
#)
