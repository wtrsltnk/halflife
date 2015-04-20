cmake_minimum_required(VERSION 2.6)

#####################################################################
# Register project
project(run-jump-retry)
#####################################################################


#####################################################################
# Build type
if(${CMAKE_BUILD_TYPE} MATCHES DEBUG)
    message(STATUS "CMAKE_BUILD_TYPE: Debug")
else()
    message(STATUS "CMAKE_BUILD_TYPE: Release")
endif(${CMAKE_BUILD_TYPE} MATCHES DEBUG)
#####################################################################

add_subdirectory(dlls)
add_subdirectory(cl_dll)
