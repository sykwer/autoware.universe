cmake_minimum_required(VERSION 3.14)
project(autoware_pid_longitudinal_controller)

find_package(autoware_cmake REQUIRED)
autoware_package()

find_package(fmt REQUIRED)

set(PID_LON_CON_LIB ${PROJECT_NAME}_lib)
ament_auto_add_library(${PID_LON_CON_LIB} SHARED
  DIRECTORY src
)

if(BUILD_TESTING)
  set(TEST_LON_SOURCES
    test/test_pid.cpp
    test/test_smooth_stop.cpp
    test/test_longitudinal_controller_utils.cpp
  )
  set(TEST_LONGITUDINAL_CONTROLLER_EXE test_longitudinal_controller)
  ament_add_ros_isolated_gtest(${TEST_LONGITUDINAL_CONTROLLER_EXE} ${TEST_LON_SOURCES})
  target_link_libraries(${TEST_LONGITUDINAL_CONTROLLER_EXE} ${PID_LON_CON_LIB})
endif()

ament_auto_package(
  INSTALL_TO_SHARE
  config
)
