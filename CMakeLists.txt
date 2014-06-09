cmake_minimum_required(VERSION 2.8.3)
project(robot_state_chain_publisher)

find_package(catkin REQUIRED COMPONENTS roscpp kdl_parser sensor_msgs tf tf_conversions)
find_package(Boost REQUIRED COMPONENTS system)
find_package(orocos_kdl)

catkin_package(
   LIBRARIES ${PROJECT_NAME})

include_directories(include ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})

add_library(${PROJECT_NAME} src/joint_state_listener.cpp src/robot_state_publisher.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

add_executable(state_chain_publisher src/state_publisher.cpp)
target_link_libraries(state_chain_publisher ${Boost_LIBRARIES} ${PROJECT_NAME} ${orocos_kdl_LIBRARIES})

# Install library
INSTALL (TARGETS ${PROJECT_NAME} DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
# Install executable
INSTALL (TARGETS state_chain_publisher
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
