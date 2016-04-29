cmake_minimum_required(VERSION 2.8.2)

project(re)

include(CheckIncludeFiles)

set(CMAKE_VERBOSE_MAKEFILE ON)

check_include_files(poll.h HAVE_POLL_H)
check_include_files(unistd.h HAVE_UNISTD_H)
check_include_files(sys/time.h HAVE_SYS_TIME_H)
check_include_files(sys/sysctl.h HAVE_SYS_SYSCTL_H)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR}/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

add_definitions("-DHAVE_CONFIG_H")
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)

add_subdirectory(src)
