cmake_minimum_required(VERSION 2.8.3)
project(jsk_tools)

find_package(catkin REQUIRED)
set(ROS_BUILD_TYPE RelWithDebInfo)
catkin_package(
  CATKIN_DEPENDS #
  LIBRARIES #
  INCLUDE_DIRS #
  DEPENDS #
  CFG_EXTRAS download_package.cmake
  )

install(DIRECTORY src test bin
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  )
install(DIRECTORY bin
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  USE_SOURCE_PERMISSIONS
  )

add_custom_command(OUTPUT ${CATKIN_DEVEL_PREFIX}/${CATKIN_GLOBAL_BIN_DESTINATION}/ros_console.py
  COMMAND cmake -E make_directory ${CATKIN_DEVEL_PREFIX}/${CATKIN_GLOBAL_BIN_DESTINATION}
  COMMAND cmake -E copy ${PROJECT_SOURCE_DIR}/bin/ros_console.py ${CATKIN_DEVEL_PREFIX}/${CATKIN_GLOBAL_BIN_DESTINATION}/
  DEPENDS ${PROJECT_SOURCE_DIR}/bin/ros_console.py)
add_custom_target(install_ros_console ALL DEPENDS ${CATKIN_DEVEL_PREFIX}/${CATKIN_GLOBAL_BIN_DESTINATION}/ros_console.py)
install(PROGRAMS bin/ros_console.py
  DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION})