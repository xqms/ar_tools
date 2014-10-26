
cmake_minimum_required(VERSION 2.8)

project(ar_pose)

find_package(catkin REQUIRED
	ar_tools_msgs
	artoolkit
	visualization_msgs
	geometry_msgs
	tf
	resource_retriever
	image_transport
	cv_bridge
	message_generation
)

catkin_package(
 CATKIN_DEPENDS ar_tools_msgs visualization_msgs geometry_msgs tf resource_retriever image_transport cv_bridge message_runtime
)

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
