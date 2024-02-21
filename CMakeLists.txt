# Set the name and the supported language of the project
project(hello-world C)

# Set the minimum version of cmake required to build this project
cmake_minimum_required(VERSION 3.10)

# Use the package PkgConfig to detect GTK+ headers/library files
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK4 REQUIRED gtk4)

add_executable(hello main.c)
target_link_libraries(hello ${GTK4_LIBRARIES})

# Add other flags to the compiler
#target_compile_definitions(hello PRIVATE ${GTK3_CFLAGS_OTHER})

# Setup CMake to use GTK+, tell the compiler where to look for headers
# and to the linker where to look for libraries
target_include_directories(hello PRIVATE ${GTK4_INCLUDE_DIRS})
target_link_directories(hello PRIVATE ${GTK4_LIBRARY_DIRS})
