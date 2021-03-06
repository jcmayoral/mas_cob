cmake_minimum_required(VERSION 2.8.3)
project(mas_lwr_kinematics)
set (CMAKE_CXX_STANDARD 11)

find_package(cmake_modules REQUIRED)
find_package(Eigen3 REQUIRED)

find_package(catkin REQUIRED COMPONENTS
  moveit_core
  pluginlib
  roscpp
  tf_conversions
)

include_directories(
  include
  #SYSTEM
  ${catkin_INCLUDE_DIRS}
  ${EIGEN_INCLUDE_DIRS}
)

catkin_package()

set(IKFAST_LIBRARY_NAME lwr_moveit_ikfast_plugin)

find_package(LAPACK REQUIRED)

add_library(${IKFAST_LIBRARY_NAME}
  src/lwr_ikfast_moveit_plugin.cpp
  src/solution_comparator.cpp
)
target_link_libraries(${IKFAST_LIBRARY_NAME} ${catkin_LIBRARIES} ${Boost_LIBRARIES} ${LAPACK_LIBRARIES})

install(TARGETS ${IKFAST_LIBRARY_NAME} LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
install(DIRECTORY include/ DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})

install(
  FILES
    lwr_moveit_ikfast_plugin_description.xml
  DESTINATION
     ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
