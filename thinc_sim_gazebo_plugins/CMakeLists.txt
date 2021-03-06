cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

rosbuild_add_boost_directories()

rosbuild_add_library(diffdrive_plugin_6w src/diffdrive_plugin_6w.cpp)
rosbuild_link_boost(diffdrive_plugin_6w thread)

rosbuild_add_library(reset_plugin src/reset_plugin.cpp)

#some unknown error!!!
rosbuild_add_library(hector_gazebo_ros_imu src/gazebo_ros_imu.cpp)
rosbuild_link_boost(hector_gazebo_ros_imu thread)

rosbuild_add_library(hector_gazebo_ros_magnetic src/gazebo_ros_magnetic.cpp)
rosbuild_add_library(hector_gazebo_ros_gps src/gazebo_ros_gps.cpp)
rosbuild_add_library(hector_gazebo_ros_sonar src/gazebo_ros_sonar.cpp)


rosbuild_add_library(hector_gazebo_ros_baro src/gazebo_ros_baro.cpp)

rosbuild_add_library(hector_gazebo_quadrotor_simple_controller src/quadrotor_simple_controller.cpp)

rosbuild_add_library(hector_gazebo_quadrotor_state_controller src/quadrotor_state_controller.cpp)

#Add the grid_floor file
#rosbuild_add_library(grid_floor src/grid_floor.cpp)

rosbuild_add_executable(test_trajectory src/test_trajectory.cpp)

add_subdirectory(urdf)


#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
rosbuild_gensrv()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})
