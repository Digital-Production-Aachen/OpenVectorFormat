load("@rules_proto//proto:defs.bzl", "proto_library")
load("@rules_proto_grpc//csharp:defs.bzl", "csharp_proto_library")
load("@rules_proto_grpc//csharp:defs.bzl", "csharp_proto_compile")
load("@rules_proto_grpc//python:defs.bzl", "python_proto_library")
load("@rules_proto_grpc//python:defs.bzl", "python_proto_compile")
load("@rules_proto_grpc//cpp:defs.bzl", "cpp_proto_library")
load("@rules_proto_grpc//cpp:defs.bzl", "cpp_proto_compile")
load("@rules_proto_grpc//go:defs.bzl", "go_proto_library")
load("@rules_proto_grpc//go:defs.bzl", "go_proto_compile")



proto_library(
      name = "openvectorformat_proto",
      srcs = ["open_vector_format.proto"],
      visibility = ["//visibility:public"],
)

'''csharp_proto_library(
      name = "openvectorformat_csharp.dll",
      protos = [":openvectorformat_proto"],
)'''


csharp_proto_compile(
      name = "openvectorformat_csharp",
      protos = [":openvectorformat_proto"],
      visibility = ["//visibility:public"],
)

python_proto_library(
      name = "openvectorformat_python_standalone",
      protos = [":openvectorformat_proto"],
      visibility = ["//visibility:public"],
)
python_proto_compile(
      name = "openvectorformat_python",
      protos = [":openvectorformat_proto"],
      visibility = ["//visibility:public"],
)

cpp_proto_library(
      name = "openvectorformat_cpp_standalone",
      protos = [":openvectorformat_proto"],
      visibility = ["//visibility:public"],
)
cpp_proto_compile(
      name = "openvectorformat_cpp",
      protos = [":openvectorformat_proto"],
      visibility = ["//visibility:public"],
)

go_proto_library(
      name = "openvectorformat_go_standalone",
      importpath = "github.com/digital-production-aachen/openvectorformat/proto",
      protos = [":openvectorformat_proto"],
      visibility = ["//visibility:public"],
)
go_proto_compile(
      name = "openvectorformat_go",
      protos = [":openvectorformat_proto"],
      visibility = ["//visibility:public"],
)
