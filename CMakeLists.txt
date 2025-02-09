# Set the name and the supported language of the project
project(hello-world C)

# Set the minimum version of cmake required to build this project
cmake_minimum_required(VERSION 3.10)

# Use the package PkgConfig to detect GTK+ headers/library files
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK4 REQUIRED gtk4)

#message("gtk4 libraries: " ${GTK4_LIBRARIES})
#message("gtk4 libraries dirs: " ${GTK4_LIBRARY_DIRS})
#message("gtk4 include dir: " ${GTK4_INCLUDE_DIRS})

# Find the libgpiod library
find_library(GPIOD_LIBRARY gpiod)

# Find the libgpiod header files
find_path(GPIOD_INCLUDE_DIR gpiod.h)

#message ("gpiod library: " ${GPIOD_LIBRARY})
#message ("gpiod include dir: " ${GPIOD_INCLUDE_DIR})

# Check if the library and headers were found
if (NOT GPIOD_LIBRARY OR NOT GPIOD_INCLUDE_DIR)
    message(FATAL_ERROR "libgpiod not found")
endif()

add_executable(hello main.c)
target_link_libraries(hello ${GTK4_LIBRARIES} ${GPIOD_LIBRARY})

# Add other flags to the compiler
#target_compile_definitions(hello PRIVATE ${GTK3_CFLAGS_OTHER})

# Setup CMake to use GTK+, tell the compiler where to look for headers
# and to the linker where to look for libraries
target_include_directories(hello PRIVATE ${GTK4_INCLUDE_DIRS} ${GPIOD_INCLUDE_DIR})
target_link_directories(hello PRIVATE ${GTK4_LIBRARY_DIRS})
