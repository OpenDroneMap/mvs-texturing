cmake_minimum_required(VERSION 3.1)

project(Texturing)
include(ExternalProject)

if(NOT CMAKE_BUILD_TYPE)
    message(STATUS "Setting build type to 'RELWITHDEBINFO' as none was specified.")
    set(CMAKE_BUILD_TYPE RELWITHDEBINFO)
endif()

#Search for TBB library (release build)
set(CMAKE_BUILD_TYPE_BACKUP ${CMAKE_BUILD_TYPE})
set(CMAKE_BUILD_TYPE RELEASE)
FIND_PACKAGE(TBB REQUIRED)
set(CMAKE_BUILD_TYPE ${CMAKE_BUILD_TYPE_BACKUP})

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED yes)
add_definitions(-DEIGEN_MPL2_ONLY)

FIND_PACKAGE(OpenMP)
if(OPENMP_FOUND)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

if(CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=native -Wall -Wextra -Wundef -pedantic")
    if( (NOT ${CMAKE_SYSTEM_PROCESSOR} STREQUAL "aarch64") AND (NOT ${CMAKE_SYSTEM_PROCESSOR} STREQUAL "arm64") )
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -mfpmath=sse -funroll-loops")
    endif()
endif()

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

set(MVE_ROOT "${CMAKE_CURRENT_SOURCE_DIR}/../mve" CACHE PATH "Path to MVE root")
find_package(MVE REQUIRED)
find_package(PNG REQUIRED)
find_package(JPEG REQUIRED)
find_package(TIFF REQUIRED)

if (WIN32)
    add_definitions(-DWIN32_LEAN_AND_MEAN -DVC_EXTRALEAN -DNOMINMAX)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
endif()

add_subdirectory(elibs)
include_directories(SYSTEM
    ${CMAKE_SOURCE_DIR}/elibs/rayint/libs
    ${MVE_INCLUDE_DIRS}
    ${CMAKE_SOURCE_DIR}/elibs/eigen
    ${CMAKE_SOURCE_DIR}/elibs/mapmap/
    ${CMAKE_SOURCE_DIR}/elibs/mapmap/mapmap
    ${CMAKE_SOURCE_DIR}/elibs/mapmap/ext/dset
)

include_directories(
    libs
)

add_subdirectory(libs)
add_subdirectory(apps)
