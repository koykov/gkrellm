cmake_minimum_required(VERSION 3.14)
project(gkrellm C)

set(CMAKE_C_STANDARD 99)

include_directories(.)

set(SHARED ../shared)
include_directories(${SHARED})

find_package(PkgConfig REQUIRED)
find_package(GTK2 REQUIRED gtk)
pkg_search_module(GLIB REQUIRED glib-2.0)
include_directories(${GLIB_INCLUDE_DIRS})
pkg_check_modules(PC_HB REQUIRED harfbuzz)
include_directories(${PC_HB_INCLUDE_DIRS})

add_executable(gkrellm main.c config.c ${SHARED}/log.c)

target_link_libraries(gkrellm PRIVATE GTK2::gtk)
