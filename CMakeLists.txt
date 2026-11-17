cmake_minimum_required(VERSION 3.20)
project(ConstitutionalSEF_CPP LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find Protobuf
find_package(Protobuf REQUIRED)
include_directories(${Protobuf_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

# Generate C++ files from Protobuf IDL
protobuf_generate_cpp(PROTO_SRCS PROTO_HDRS schema.proto)

# Executable Target (Tier 3)
add_executable(sef_runtime main.cpp ${PROTO_SRCS} ${PROTO_HDRS})
target_link_libraries(sef_runtime PRIVATE ${Protobuf_LIBRARIES})
