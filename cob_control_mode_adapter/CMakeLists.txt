cmake_minimum_required(VERSION 2.8.3)
project(cob_control_mode_adapter)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  control_msgs
  controller_manager_msgs
)

find_package(Boost REQUIRED COMPONENTS thread )

catkin_package(
  CATKIN_DEPENDS roscpp std_msgs control_msgs controller_manager_msgs
)

###########
## Build ##
###########

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
)

# Declare a cpp executable
add_executable(cob_control_mode_adapter_node src/cob_control_mode_adapter_node.cpp)
add_dependencies(cob_control_mode_adapter_node controller_manager_msgs_gencpp)

# Specify libraries to link a library or executable target against
target_link_libraries(cob_control_mode_adapter_node
 ${catkin_LIBRARIES}
 ${Boost_LIBRARIES}
)

#############
## Install ##
#############

# Mark executables and/or libraries for installation
install(TARGETS cob_control_mode_adapter_node
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
