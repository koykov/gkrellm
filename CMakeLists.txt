cmake_minimum_required(VERSION 3.14)
project(gkrellm C)

set(CMAKE_C_STANDARD 99)

#set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -lgmodule-2.0")

include_directories(.)

set(SRC ./src)
set(SHARED ./shared)
set(PIXMAPS ./pixmaps)
include_directories(${SRC})
include_directories(${SHARED})
include_directories(${PIXMAPS})

find_package(PkgConfig REQUIRED)
find_package(GTK2 REQUIRED gtk)
pkg_search_module(GLIB REQUIRED glib-2.0)
include_directories(${GLIB_INCLUDE_DIRS})
pkg_check_modules(PC_HB REQUIRED harfbuzz)
include_directories(${PC_HB_INCLUDE_DIRS})

add_executable(gkrellm
        ${SRC}/main.c
        ${SRC}/config.c
        ${SRC}/alerts.c
        ${SRC}/base64.c
        ${SRC}/battery.c
        ${SRC}/chart.c
        ${SRC}/client.c
        ${SRC}/clock.c
        ${SRC}/cpu.c
        ${SRC}/deprecated.c
        ${SRC}/disk.c
        ${SRC}/fs.c
        ${SRC}/gui.c
        ${SRC}/hostname.c
        ${SRC}/inet.c
        ${SRC}/krell.c
        ${SRC}/mail.c
        ${SRC}/md5c.c
        ${SRC}/mem.c
        ${SRC}/net.c
        ${SRC}/panel.c
        ${SRC}/pixops.c
        ${SRC}/plugins.c
        ${SRC}/proc.c
        ${SRC}/sensors.c
        ${SRC}/sysdeps-unix.c
        ${SRC}/uptime.c
        ${SRC}/utils.c
        ${SRC}/winops-x11.c

        ${SHARED}/log.c)

target_include_directories(gkrellm PUBLIC shared)

target_link_libraries(gkrellm PRIVATE GTK2::gtk -lgmodule-2.0 -lX11 -lm -lssl -lcrypto)
