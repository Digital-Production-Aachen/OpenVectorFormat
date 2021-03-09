load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_proto_grpc",
    sha256 = "fa7a59e0d1527ac69be652407b457ba1cb40700752a3ee6cc2dd25d9cb28bb1a",
    strip_prefix = "rules_proto_grpc-3.1.0",
    urls = ["https://github.com/rules-proto-grpc/rules_proto_grpc/archive/3.1.0.tar.gz"],
)

load("@rules_proto_grpc//:repositories.bzl", "rules_proto_grpc_toolchains", "rules_proto_grpc_repos")
rules_proto_grpc_toolchains()
rules_proto_grpc_repos()

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
rules_proto_dependencies()
rules_proto_toolchains()


## C SHARP RULES
load("@rules_proto_grpc//csharp:repositories.bzl", rules_proto_grpc_csharp_repos = "csharp_repos")

rules_proto_grpc_csharp_repos()

load("@io_bazel_rules_dotnet//dotnet:deps.bzl", "dotnet_repositories")

dotnet_repositories()

load(
    "@io_bazel_rules_dotnet//dotnet:defs.bzl",
    "dotnet_register_toolchains",
    "dotnet_repositories_nugets",
)

dotnet_register_toolchains()

dotnet_repositories_nugets()

load("@rules_proto_grpc//csharp/nuget:nuget.bzl", "nuget_rules_proto_grpc_packages")

nuget_rules_proto_grpc_packages()


## PYTHON

load("@rules_proto_grpc//python:repositories.bzl", rules_proto_grpc_python_repos = "python_repos")

rules_proto_grpc_python_repos()

## C++
load("@rules_proto_grpc//cpp:repositories.bzl", rules_proto_grpc_cpp_repos = "cpp_repos")

rules_proto_grpc_cpp_repos()

## GOLANG

load("@rules_proto_grpc//:repositories.bzl", "bazel_gazelle", "io_bazel_rules_go")  # buildifier: disable=same-origin-load

io_bazel_rules_go()

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(
    version = "1.15.8",
)

bazel_gazelle()

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()

load("@rules_proto_grpc//go:repositories.bzl", rules_proto_grpc_go_repos = "go_repos")

rules_proto_grpc_go_repos()


