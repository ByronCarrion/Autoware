cmake_minimum_required(VERSION 2.8.3)
project(as)

find_package(
        catkin REQUIRED COMPONENTS
        roscpp
        std_msgs
        geometry_msgs
        automotive_platform_msgs
        dbw_mkz_msgs
)

catkin_package(
        CATKIN_DEPENDS
        roscpp
        std_msgs
        geometry_msgs
        automotive_platform_msgs
        dbw_mkz_msgs
)

SET(CMAKE_CXX_FLAGS "-O2 -g -Wall ${CMAKE_CXX_FLAGS}")

include_directories(
        ${catkin_INCLUDE_DIRS}
)

add_executable(pacmod_interface
        nodes/pacmod_interface/pacmod_interface_node.cpp
        nodes/pacmod_interface/pacmod_interface.cpp
        )
target_link_libraries(pacmod_interface ${catkin_LIBRARIES})
add_dependencies(pacmod_interface ${catkin_EXPORTED_TARGETS})

install(TARGETS pacmod_interface
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
        )

install(DIRECTORY launch/
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
        PATTERN ".svn" EXCLUDE)
