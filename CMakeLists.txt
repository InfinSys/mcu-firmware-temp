
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

if(DEFINED CACHE{${LOCAL_PROJECT_SCOPE}_PROJECT_TESTING} AND ${LOCAL_PROJECT_SCOPE}_PROJECT_TESTING)
	message(STATUS "${LOCAL_CMAKE_PROJECT_NAME} testing - enabled")
	set(UNIT_TESTING ON)
	enable_testing()
else()
	message(STATUS "${LOCAL_CMAKE_PROJECT_NAME} testing - disabled")
endif()


#include_directories("${CMAKE_CURRENT_SOURCE_DIR}/include")


if(UNIT_TESTING)
	add_subdirectory(3rdparty/googletest)
	add_subdirectory(3rdparty/benchmark)
	add_subdirectory(tests)
endif()
