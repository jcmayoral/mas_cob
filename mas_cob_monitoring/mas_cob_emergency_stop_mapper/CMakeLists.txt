cmake_minimum_required(VERSION 2.8.3)
project(mas_cob_emergency_stop_mapper)

find_package(catkin REQUIRED
  COMPONENTS
    roscpp
    std_msgs
    cob_relayboard
)

catkin_package(
  CATKIN_DEPENDS
    std_msgs
    cob_relayboard
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_executable(emergency_stop_mapper
  ros/src/emergency_stop_mapper.cpp
)

target_link_libraries(emergency_stop_mapper
  ${catkin_LIBRARIES}
)
add_dependencies(emergency_stop_mapper
  ${catkin_EXPORTED_TARGETS}
)

### INSTALL ###
install(TARGETS emergency_stop_mapper
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
