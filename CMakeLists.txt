cmake_minimum_required(VERSION 3.0.2)
project(implicit_lidar_network)


SET(CMAKE_BUILD_TYPE Release)
#SET(CMAKE_BUILD_TYPE Debug)
ADD_COMPILE_OPTIONS(-std=c++11)
if(CMAKE_BUILD_TYPE STREQUAL "Release")
    ADD_COMPILE_OPTIONS(-O3)
endif()

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
    roscpp
    rospy
    sensor_msgs
    pcl_ros
)

FIND_PACKAGE(Eigen3 REQUIRED)

INCLUDE(FindOpenMP)
if(OPENMP_FOUND)
    SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()
ADD_DEFINITIONS(-DOPENMP)


catkin_package(
)

include_directories(
    include
    ${catkin_INCLUDE_DIRS}
    ${EIGEN3_INCLUDE_DIR}
)

add_subdirectory(extern/pybind11)
pybind11_add_module(voxelizer SHARED src/voxelizer.cpp)
set_target_properties(voxelizer PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/python_src
)