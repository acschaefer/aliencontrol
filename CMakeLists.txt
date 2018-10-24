cmake_minimum_required(VERSION 2.8.3)
project(aliencontrol)

## Find catkin macros and libraries.
## If COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages.
find_package(catkin REQUIRED COMPONENTS
    rospy
)

###################################
## catkin-specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package.
## Declare things to be passed to dependent projects.
## INCLUDE_DIRS: uncomment this if your package contains header files.
## LIBRARIES: libraries you create in this project that dependent projects also need.
## CATKIN_DEPENDS: catkin_packages dependent projects also need.
## DEPENDS: system dependencies of this project that dependent projects also need.
catkin_package(
    CATKIN_DEPENDS rospy
)

#############
## Install ##
#############
# All install targets should use catkin DESTINATION variables.
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html.

# Mark executable scripts (Python etc.) for installation.
# In contrast to setup.py, you can choose the destination.
install(PROGRAMS
    aliencontrol
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
