cmake_minimum_required(VERSION 2.8.3)

project(trajectory_planning_srvs)



# check c++11 / c++0x
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    #set(CMAKE_CXX_FLAGS "-std=c++11")
    add_definitions(-std=c++11)
elseif(COMPILER_SUPPORTS_CXX0X)
    #set(CMAKE_CXX_FLAGS "-std=c++0x")
    add_definitions(-std=c++0x)
else()
    message(FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()





find_package(catkin REQUIRED
                COMPONENTS message_generation std_msgs geometry_msgs nav_msgs robot_geometry_msgs)



add_service_files(
    DIRECTORY
        srv
    FILES
        GenerateCollisionFreePath.srv
        CheckCollisionFreePath.srv
        GenerateBetterCollisionFreePath.srv
        GetTrajectoryPoints.srv


)



generate_messages(DEPENDENCIES std_msgs geometry_msgs nav_msgs robot_geometry_msgs)




catkin_package(
    CATKIN_DEPENDS message_runtime std_msgs geometry_msgs nav_msgs robot_geometry_msgs
	)



#include_directories(${catkin_INCLUDE_DIRS})

