cmake_minimum_required(VERSION 3.10)
project(MultiDockerServerPipeline VERSION 1.0.0)

include_directories(/usr/include)
find_package(libssh CONFIG REQUIRED)

add_subdirectory(ssh_server)
add_subdirectory(validator)

add_executable(ssh_deploy main.cpp)

target_include_directories(ssh_server PUBLIC ssh_server)
target_include_directories(validator PUBLIC validator)

target_link_libraries(ssh_deploy ssh_server)
target_link_libraries(ssh_deploy validator)
target_link_libraries(ssh_deploy ssh)