cmake_minimum_required(VERSION 2.8.3)
project(iri_visual_servo_msgs)

find_package(catkin REQUIRED)
find_package(catkin REQUIRED COMPONENTS geometry_msgs message_generation)

add_message_files(
  DIRECTORY msg
  FILES
	ARMarker.msg
	ARMarkers.msg
)

generate_messages(
  DEPENDENCIES
  geometry_msgs
)

catkin_package(
 CATKIN_DEPENDS geometry_msgs message_runtime
)