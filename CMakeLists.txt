
#==============================
#
#     Root CMakeLists.txt
#
#==============================



cmake_minimum_required(VERSION 3.6 FATAL_ERROR)

set(LOCAL_CMAKE_PROJECT_NAME "Demo_Core")

project("${LOCAL_CMAKE_PROJECT_NAME}" VERSION 0.0.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")

set(LOCAL_PROJECT_SCOPE "DEMO")


set(UNIT_TESTING OFF)
set(BENCHMARKING OFF)

if(DEFINED CACHE{${LOCAL_PROJECT_SCOPE}_PROJECT_TESTING} AND ${LOCAL_PROJECT_SCOPE}_PROJECT_TESTING)
	message(STATUS "${LOCAL_CMAKE_PROJECT_NAME} host-side testing - enabled")
	set(UNIT_TESTING ON)
	enable_testing()
	add_subdirectory(3rdparty/googletest)
else()
	message(STATUS "${LOCAL_CMAKE_PROJECT_NAME} host-side testing - disabled")
endif()

if(DEFINED CACHE{${LOCAL_PROJECT_SCOPE}_PROJECT_BENCHMARK} AND ${LOCAL_PROJECT_SCOPE}_PROJECT_BENCHMARK)
	message(STATUS "${LOCAL_CMAKE_PROJECT_NAME} host-side benchmarking - enabled")
	set(BENCHMARKING ON)
	add_subdirectory(3rdparty/benchmark)
else()
	message(STATUS "${LOCAL_CMAKE_PROJECT_NAME} host-side benchmarking - disabled")
endif()


#include_directories("${CMAKE_CURRENT_SOURCE_DIR}/include")


if(UNIT_TESTING OR BENCHMARKING)
	add_subdirectory(tests/host)
endif()
