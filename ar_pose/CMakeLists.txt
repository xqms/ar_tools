
cmake_minimum_required(VERSION 2.8)

project(ar_pose)

find_package(catkin REQUIRED
	visualization_msgs
	artoolkit
	geometry_msgs
	tf
	resource_retriever
	image_transport
	cv_bridge
	message_generation
)


add_message_files(
  DIRECTORY msg
  FILES
	ARMarker.msg
	ARMarkers.msg
)

generate_messages(DEPENDENCIES
	geometry_msgs
)

catkin_package(
#  INCLUDE_DIRS 
#  LIBRARIES 
 CATKIN_DEPENDS visualization_msgs artoolkit geometry_msgs tf resource_retriever image_transport cv_bridge message_runtime
#  DEPENDS 
)

# This hack is only to allow the rosmsg tool to locate the messages genererated by the actions, so that the IRI scripts can
# locate them when adding actions to a node.
add_custom_target(ar_pose_copy_msgs ALL)
add_custom_command(TARGET ar_pose_copy_msgs POST_BUILD
COMMAND rsync -aq ${CATKIN_DEVEL_PREFIX}/share/${PROJECT_NAME}/ ${CMAKE_CURRENT_SOURCE_DIR}/msg/)
add_dependencies(ar_pose_copy_msgs ar_pose_msgs_generate_messages_cpp)


include_directories(${catkin_INCLUDE_DIRS} include)

add_executable(ar_single
	src/ar_single.cpp
	src/object.cpp
)
target_link_libraries(ar_single
	${catkin_LIBRARIES}
)
add_dependencies(ar_single
	${PROJECT_NAME}_generate_messages_cpp
	${artoolkit_EXPORTED_TARGETS}
)

add_executable(ar_multi
	src/ar_multi.cpp
	src/object.cpp
)
target_link_libraries(ar_multi
	${catkin_LIBRARIES}
)
add_dependencies(ar_multi
	${PROJECT_NAME}_generate_messages_cpp
	${artoolkit_EXPORTED_TARGETS}
)
