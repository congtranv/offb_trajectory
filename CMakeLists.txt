cmake_minimum_required(VERSION 3.0.2)
project(offb_trajectory)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  mavros_msgs
  roscpp
  roslaunch
  rospy
  std_msgs
)

catkin_package(
  INCLUDE_DIRS include
  # LIBRARIES offb_trajectory
  CATKIN_DEPENDS geometry_msgs mavros_msgs roscpp roslaunch rospy std_msgs
  # DEPENDS system_lib
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

roslaunch_add_file_check(launch)

add_library(offb_trajectory_lib
  src/offb_trajectory.cpp
)

target_link_libraries(offb_trajectory_lib
  ${catkin_LIBRARIES}
)

add_executable(offb_trajectory src/offb_trajectory_node.cpp)
target_link_libraries(offb_trajectory
  offb_trajectory_lib
)

add_executable(setmode src/set_mode.cpp)
target_link_libraries(setmode
  ${catkin_LIBRARIES}
)