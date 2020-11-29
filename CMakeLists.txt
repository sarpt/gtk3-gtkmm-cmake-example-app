# Set the name and the supported language of the project
project(GTKTut CXX)

# Set the minimum version of cmake required to build this project
cmake_minimum_required(VERSION 3.19.1)

# Use the package PkgConfig to detect GTK+ & GTKMM headers/library files 
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK3 REQUIRED gtk+-3.0)
pkg_check_modules(GTKMM3 REQUIRED gtkmm-3.0)

# Find all hpp and cpp src files and save in $SOURCE_LIST
file(GLOB SOURCE_LIST
    "src/*.hpp"
    "src/*.cpp"
)

# Setup CMake to use GTK+, tell the compiler where to look for headers
# and to the linker where to look for libraries.
# The variables are set by calling PKG_CHECK_MODULES with GTK3 and GTK3MM
include_directories(${GTK3_INCLUDE_DIRS} ${GTKMM3_INCLUDE_DIRS})
link_directories(${GTK3_LIBRARY_DIRS} ${GTKMM3_LIBRARY_DIRS})

# Add other flags to the compiler
add_definitions(${GTK3_CFLAGS_OTHER} ${GTKMM3_CFLAGS_OTHER})

# Add an executable compiled from hello.c
add_executable(gtk-tut ${SOURCE_LIST})

# Link the target to the GTK+ libraries
target_link_libraries(gtk-tut ${GTK3_LIBRARIES} ${GTKMM3_LIBRARIES})
