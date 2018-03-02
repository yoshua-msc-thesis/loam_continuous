cmake_minimum_required(VERSION 2.8.3)
project(loam_continuous)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  nav_msgs
  sensor_msgs
  roscpp
  rospy
  std_msgs
  pcl_conversions
  pcl_ros
)

find_package(Eigen3 REQUIRED QUIET)
find_package(PCL REQUIRED QUIET)
set(OpenCV_DIR $ENV{OPENCV2_INSTALL_DIR})
find_package(OpenCV 2 REQUIRED QUIET)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIR}
  ${PCL_INCLUDE_DIRS}
)

LIST(APPEND LINK_LIBS
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
  ${OpenCV_LIBRARIES}
)

catkin_package(
  CATKIN_DEPENDS geometry_msgs nav_msgs roscpp rospy std_msgs
  DEPENDS EIGEN3 PCL OpenCV
)


add_executable(scanRegistration_ct src/scanRegistration.cpp)
target_link_libraries(scanRegistration_ct ${LINK_LIBS})

add_executable(laserOdometry_ct src/laserOdometry.cpp)
target_link_libraries(laserOdometry_ct ${LINK_LIBS})

add_executable(laserMapping_ct src/laserMapping.cpp)
target_link_libraries(laserMapping_ct ${LINK_LIBS})

add_executable(transformMaintenance_ct src/transformMaintenance.cpp)
target_link_libraries(transformMaintenance_ct ${LINK_LIBS})


