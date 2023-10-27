cmake_minimum_required(VERSION 3.18)

project(Adept
  VERSION 0.1.0
  DESCRIPTION "Accelerated demonstrator of electromagnetic Particle Transport"
  LANGUAGES C CXX)

message(STATUS ">>> Top level call to find VecGeom")
find_package(VecGeom REQUIRED)

message(STATUS ">>> Top level call to find Geant4")
find_package(Geant4 QUIET)

if(NOT Geant4_FOUND)
  message(STATUS "Did not find Geant4")
endif()

# This is the G4HepEM part
add_subdirectory(externals)

