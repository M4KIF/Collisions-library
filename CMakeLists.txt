cmake_minimum_required(VERSION 3.12)

cmake_policy(set CMP0048 new)

project (Collisions)

set(CMAKE_CXX_STANDARD 11)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/AABB)
