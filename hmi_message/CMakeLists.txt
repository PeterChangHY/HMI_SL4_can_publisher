cmake_minimum_required(VERSION 2.8.12)

project(hmi_message)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_VERBOSE_MAKEFILE ON)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

# set drive root from environment, else use default
#if(NOT DEFINED DRIVE_ROOT)
#if(DEFINED ENV{DRIVE_ROOT})
#set(DRIVE_ROOT "$ENV{DRIVE_ROOT}")
#else()
#set(DRIVE_ROOT "/opt/plusai")
#endif()
#endif()
#message(STATUS "DRIVE_ROOT: ${DRIVE_ROOT}")

#list(APPEND CMAKE_PREFIX_PATH "${DRIVE_ROOT}")
#find_package(drive REQUIRED)
#include_directories(${drive_INCLUDE_DIRS})
#include_directories(${drive_INCLUDE_DIRS}/common)
#include_directories(${drive_INCLUDE_DIRS}/proto)

#link_directories(${drive_LIBRARY_DIRS})

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(SRCS
    src/vehicle_status_general_info_msg.cpp
    src/obstacle_general_info_msg.cpp
    src/lane_general_info_msg.cpp
    src/planning_general_info_msg.cpp
)
add_library(${PROJECT_NAME}
    ${SRCS}
)


target_link_libraries(${PROJECT_NAME}
  drive_common_proto
  ${GLOG_LIBRARIES}
  ${PROTOBUF_LIBRARIES}
)

#################### test #######################

create_test(utils)
create_test(vehicle_status_msg)
create_test(obstacle_msg)
create_test(lane_msg)
create_test(planning_msg)

#################### install ####################
install(DIRECTORY  "include/" DESTINATION "include/hmi_message")
