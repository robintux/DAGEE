# Copyright (c) 2018-Present Advanced Micro Devices, Inc. See LICENSE.TXT for terms.

cmake_minimum_required(VERSION 3.1)

project(DAGEE-examples
  VERSION 0.1)

if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE RelWithDebInfo)
endif()

include(cmakeUtils/common.cmake)
include(cmakeUtils/enableCompilerWarnings.cmake)
include(CTest)


set(CMAKE_CXX_STANDARD 11) # C++11...
set(CMAKE_CXX_STANDARD_REQUIRED ON) #...is required...
set(CMAKE_CXX_EXTENSIONS OFF) #...without compiler extensions like gnu++11

if(CMAKE_CXX_COMPILER MATCHES "hipcc")
  set(HAVE_HIP ON)
endif()

include(cmakeUtils/addATMI.cmake)
include(cmakeUtils/rocmVersion.cmake)

defineCMakeVar(DAGEE_ROOT "DAGEE-lib")

if(DAGEE_ROOT) 
  include_directories(${DAGEE_ROOT}/include)
endif()

include_directories(cppUtils/include)

add_subdirectory(examples)

################ doxygen documentation cmake setup ############
# list all the dirs for doxygen documentaiton
set(DOXYFILE_SOURCE_DIRS "\"${CMAKE_CURRENT_SOURCE_DIR}/README.md ${CMAKE_CURRENT_SOURCE_DIR}/doc ${CMAKE_CURRENT_SOURCE_DIR}/examples ${CMAKE_CURRENT_SOURCE_DIR}/DAGEE-lib ${CMAKE_CURRENT_SOURCE_DIR}/cppUtils/\"")

include(cmakeUtils/runDoxygen.cmake)

