cmake_minimum_required(VERSION 3.18)

project(Adept
  VERSION 0.1.0
  DESCRIPTION "Accelerated demonstrator of electromagnetic Particle Transport"
  LANGUAGES C CXX)

# - Include needed custom/core modules
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
include(CMakeSettings)
#include(CTest)

# - Core/C++/CUDA build and dependency settings
# For single-mode generators, default to Optimized with Debug if nothing is specified
if(NOT CMAKE_CONFIGURATION_TYPES)
  set(__DEFAULT_CMAKE_BUILD_TYPE RelWithDebInfo)
  if(CMAKE_BUILD_TYPE)
    set(__DEFAULT_CMAKE_BUILD_TYPE "${CMAKE_BUILD_TYPE}")
  endif()
  set(CMAKE_BUILD_TYPE "${__DEFAULT_CMAKE_BUILD_TYPE}"
    CACHE STRING "Choose the type of build, options are: None Release MinSizeRel Debug RelWithDebInfo MinSizeRel."
    FORCE)
endif()

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CUDA_STANDARD ${CMAKE_CXX_STANDARD})
set(CMAKE_CUDA_STANDARD_REQUIRED ${CMAKE_CXX_STANDARD_REQUIRED})
set(CMAKE_CUDA_EXTENSIONS OFF)
set(CMAKE_INCLUDE_DIRECTORIES_PROJECT_BEFORE ON)

find_package(VecCore ${VecCore_VERSION} REQUIRED)
message(STATUS "Using VecCore version ${VecCore_VERSION}")


message(STATUS ">>> Top level call to find VecGeom")
find_package(VecGeom REQUIRED)

message(STATUS ">>> Top level call to find Geant4")
find_package(Geant4 QUIET)

if(NOT Geant4_FOUND)
  message(STATUS "Did not find Geant4")
endif()

# This is the G4HepEM part
add_subdirectory(externals)

