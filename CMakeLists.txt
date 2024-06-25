cmake_minimum_required(VERSION 3.13)  # CMake version check
project(grpc-cpp-server)              # Create project "simple_example"
set(CMAKE_CXX_STANDARD 17)            # Enable c++14 standard

find_package(gRPC REQUIRED)
find_package(Protobuf CONFIG REQUIRED)
include_directories(${protobuf_INCLUDE_DIRS})
message("protobuf include: ${protobuf_INCLUDE_DIRS}")
add_executable(grpc-server main.cc point.proto)

protobuf_generate(
    TARGET grpc-server
    OUT_VAR PROTO_GENERATED_FILES
    IMPORT_DIRS ${CMAKE_CURRENT_SOURCE_DIR}
    PROTOC_OUT_DIR "proto"
)

target_link_libraries(grpc-server grpc::grpc)
target_include_directories(grpc-server PUBLIC
  ${CMAKE_CURRENT_BINARY_DIR}
)