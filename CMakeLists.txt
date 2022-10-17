cmake_minimum_required(VERSION 3.12)

project (Collisions-library)

add_library(
	Collisions-library
	"${CMAKE_CURRENT_SOURCE_DIR}/AABB/AABB.h"
	"${CMAKE_CURRENT_SOURCE_DIR}/AABB/AABB.cpp"
)

target_include_directories(Collisions-library PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")

