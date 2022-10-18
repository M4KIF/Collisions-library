#Making sure, that this script doesn't run on anything outdated
#Version 3.13 has the CMP0079 set to true
cmake_minimum_required(VERSION 3.13)

#Setting the variable responsible for the project name
set(PROJECT_NAME "Collisions")
project (${PROJECT_NAME})

#Adding the aabb library
add_library(
	aabb-library
	"${CMAKE_CURRENT_SOURCE_DIR}/AABB/AABB.h"
	"${CMAKE_CURRENT_SOURCE_DIR}/AABB/AABB.cpp"
)

#Giving the path to the needed includes
target_include_directories(aabb-library PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")

#Searching whether git has been initialised here
find_package(Git QUIET)

#Proceeding to the submodules checking
if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
    # Update submodules as needed
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init --recursive failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
        endif()
    endif()
endif()

#Checking for GLM submodule
if(NOT EXISTS "${PROJECT_SOURCE_DIR}/Dependencies/glm/CMakeLists.txt")
    message(FATAL_ERROR "The submodules were not downloaded! GIT_SUBMODULE was turned off or failed. Please update submodules and try again.")
endif()

#Adding the path to glm directory with a CMakeLists.txt inside
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/Dependencies/glm")

#Linking main library with the dependency
target_link_libraries(aabb-library PUBLIC glm)

