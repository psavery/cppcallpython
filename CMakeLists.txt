cmake_minimum_required(VERSION 3.1 FATAL_ERROR)

project(pybind)

set(PYTHON_EXECUTABLE python3)

set(PYBIND11_CPP_STANDARD -std=c++11)
set(CMAKE_CXX_FLAGS -std=c++11)

find_package(pybind11 CONFIG REQUIRED)

include_directories(${PYTHON_INCLUDE_DIRS})

message(STATUS "Found pybind11: ${pybind11_CONFIG}")

add_executable(test1 test.cpp)
target_link_libraries(test1 ${PYTHON_LIBRARIES})

# Copy the tests directory into the build directory after building
add_custom_command(TARGET test1 POST_BUILD
                   COMMAND ${CMAKE_COMMAND} -E copy_directory
                   ${CMAKE_SOURCE_DIR}/tests ${CMAKE_BINARY_DIR}/tests)
