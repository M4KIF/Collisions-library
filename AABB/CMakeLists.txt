cmake_minimum_required(VERSION 3.0)
project(aabb-library)

add_library(aabb AABB.h AABB.cpp)
target_include_directories(aabb PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
