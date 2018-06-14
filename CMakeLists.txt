cmake_minimum_required(VERSION 3.1)

project(hello-tbb-cmake CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Release)

set(EXTERNAL_INSTALL_DIR ${CMAKE_BINARY_DIR}/external)
link_directories(${EXTERNAL_INSTALL_DIR}/lib)
include_directories(${EXTERNAL_INSTALL_DIR}/include)

######################################################################
# Build rules for the main code
######################################################################

file(GLOB sources main.cpp)
add_executable(hello-tbb-cmake ${sources})
target_link_libraries(hello-tbb-cmake tbb)

######################################################################
# Build rules for tbb
######################################################################

include(ExternalProject)
ExternalProject_Add(
	tbb
	GIT_REPOSITORY ${CMAKE_SOURCE_DIR}/external/tbb
	GIT_TAG master
	INSTALL_DIR ${EXTERNAL_INSTALL_DIR}
	CMAKE_ARGS
	-DCMAKE_INSTALL_PREFIX:PATH=<INSTALL_DIR>
	-DTBB_BUILD_SHARED=ON
	-DTBB_BUILD_STATIC=OFF
	-DTBB_BUILD_TBBMALLOC=OFF
	-DTBB_BUILD_TBBMALLOC_PROXY=OFF
	-DTBB_BUILD_TESTS=OFF
	-DTBB_CI_BUILD=OFF
)
add_dependencies(hello-tbb-cmake tbb)
