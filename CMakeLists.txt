cmake_minimum_required(VERSION 2.6)
project(python3_orocos_kdl)

find_package(orocos_kdl REQUIRED)
find_package(PythonInterp 3 REQUIRED)
find_package(PythonLibs 3.6 REQUIRED)

find_package(Boost REQUIRED COMPONENTS python36 thread unit_test_framework)
if (NOT Boost_FOUND)
message(FATAL " Boost library not found!")
endif()

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

#include_directories(${Boost_INCLUDE_DIRS} /usr/include/python3.6m /home/arpit/catkin_ws_python3/install/include /usr/local/include/eigen3)

include_directories(${Boost_INCLUDE_DIRS} ${PYTHON_INCLUDE_DIRS} ${orocos_kdl_INCLUDE_DIRS})

add_library(PyKDL SHARED python_orocos_kdl/PyKDL.cpp)
set_target_properties(PyKDL PROPERTIES PREFIX "")
target_link_libraries(PyKDL ${Boost_LIBRARIES} ${orocos_kdl_LIBRARY})

install(FILES package.xml DESTINATION share/python_orocos_kdl)
