cmake_minimum_required(VERSION 2.8.3)
project(onboard_m600) ## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
    dji_sdk
    aerialcore_common
    roscpp
    rospy
    sensor_msgs
    std_msgs
    message_generation
  )

# Declare the service files to be built
#add_service_files(FILES
	#ProcessImg.srv
	#)

# Actually generate the language-specific message and service files
generate_messages(DEPENDENCIES std_msgs sensor_msgs)
###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if your package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
# MESSAGE(STATUS "USB INCLUDE: ${LIBUSB_1_INCLUDE_DIR}")
catkin_package(
  INCLUDE_DIRS include
  # LIBRARIES
  CATKIN_DEPENDS
    aerialcore_common
    std_msgs
    message_runtime
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
 include
 ${catkin_INCLUDE_DIRS}
)

## Declare a C++ library
# add_library(${PROJECT_NAME}
#   src/${PROJECT_NAME}/onboard-sdk-ros.cpp
# )

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
# add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Declare a C++ executable
## With catkin_make all packages are built within a single CMake context
## The recommended prefix ensures that target names across packages don't collide
# add_executable(${PROJECT_NAME}_node src/onboard-sdk-ros_node.cpp)

add_executable(m600_mission_node src/M600_mission.cpp)
target_link_libraries(m600_mission_node dji_sdk)
add_dependencies(m600_mission_node ${catkin_EXPORTED_TARGETS})

