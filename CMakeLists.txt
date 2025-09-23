cmake_minimum_required(VERSION 3.15)

# Ensure vcpkg manifest mode passes --debug to its underlying install operations.
# This must appear before the first project() call so that the vcpkg toolchain
# (loaded at project() time) can see it.
set(VCPKG_INSTALL_OPTIONS --debug)

project(hello_cpp VERSION 0.1.0 LANGUAGES CXX)

find_package(ZLIB REQUIRED)

# Require a modern C++ standard without compiler-specific extensions
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_executable(hello_cpp
    src/main.cpp
)

target_link_libraries(hello_cpp PRIVATE ZLIB::ZLIB)

# Optional install target
install(TARGETS hello_cpp RUNTIME DESTINATION bin)
