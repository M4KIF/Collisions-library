cmake_minimum_required(VERSION 3.0)
project(aabb-library)

add_library(aabb AABB.h AABB.c)
target_include_directories(glad PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
