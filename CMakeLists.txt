# cmake_minimum_required(VERSION 2.8.3)
cmake_minimum_required(VERSION 3.5)

# The project name stays the same as the original ROS1 package
project(r2robot_module_msgs)

# Add flags to support compiling on windows, since ROS2 supports it
if(NOT WIN32)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -Wall -Wextra")
endif()


# Remove the catkin dependency and add ament_cmake
find_package(ament_cmake REQUIRED)
# find_package(catkin REQUIRED COMPONENTS
#   roscpp
#   rospy
#   actionlib_msgs
#   std_msgs
#   geometry_msgs
#   sensor_msgs
#   genmsg 
#   message_generation
# )

# You specify the individual packages that are required for building like this:
find_package(builtin_interfaces REQUIRED)
# Instead of REQUIRED_COMPONENTS std_msgs
find_package(rosidl_default_generators REQUIRED)
# Instead of REQUIRED_COMPONENTS message_generation

###########
### MSGS 
###########

# # Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Float32Array.msg
#   Float64Array.msg
#   CartesianVelocity.msg
#   CartesianSpaceDMP.msg
#   JointSpaceDMP.msg
# )

# Change message files declaration to a CMake variable instead of the ROS add_message_files(...) custom macro.
# You will need to include the name of the folder since it's no longer implied.
set(msg_files
  "msg/Float32Array.msg"
  "msg/Float64Array.msg"
  "msg/CartesianVelocity.msg"
  "msg/CartesianSpaceDMP.msg"
  "msg/JointSpaceDMP.msg"
)

###########
### SRVS
###########

# ## Generate services in the 'srv' folder
# add_service_files(FILES
#   SetRobotTool.srv
#   Output.srv
#   SetDirectCartesianControl.srv
# )

# Change service files declaration to a CMake variable instead of the ROS add_service_files(...) custom macro.
# You will need to include the name of the folder here too.
set(srv_files
  "srv/SetRobotTool.srv"
  "srv/Output.srv"
  "srv/SetDirectCartesianControl.srv"
)

###########
### ACTS
###########

# # Generate actions in the 'action' folder
# add_action_files(
# DIRECTORY action	
# FILES JointDMP.action CartTrapVel.action CartLinTask.action CartDMP.action JointTrapVel.action
# )

set(act_files
  "action/JointDMP.action"
  "action/CartTrapVel.action"
  "action/CartLinTask.action"
  "action/CartDMP.action"
  "action/JointTrapVel.action"
)

##########
### GEN
##########

# ## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs
#   geometry_msgs
#   sensor_msgs
#   actionlib_msgs
# )

# Instead of calling generate_messages, use rosidl_generate_interfaces.
rosidl_generate_interfaces(${PROJECT_NAME}
    ${msg_files}
    ${srv_files}
    ${act_files}
    DEPENDENCIES builtin_interfaces
)

# Declare dependencies.
# catkin_package(
#  CATKIN_DEPENDS message_runtime 
# )
# Instead of catkin_package(CATKIN_DEPENDS ...), use ament_export_dependencies.
ament_export_dependencies(rosidl_default_runtime)

# Instead of catkin_package
ament_package()

# WIP 
# # Install the mapping rules for parameter name matches within the message.
# install(
#   FILES rosbridge_mapping_rules.yaml
#   DESTINATION share/${PROJECT_NAME}
# )