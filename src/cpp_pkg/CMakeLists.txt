cmake_minimum_required(VERSION 3.5)
project(cpp_pkg)


# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()


# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()


if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()


# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)


add_executable(${PROJECT_NAME}_node src/cpp_pub_node.cpp)
ament_target_dependencies(${PROJECT_NAME}_node rclcpp std_msgs)

add_executable(${PROJECT_NAME}_subs_node src/cpp_sub_node.cpp)
ament_target_dependencies(${PROJECT_NAME}_subs_node rclcpp std_msgs)

install(TARGETS
	${PROJECT_NAME}_node
	${PROJECT_NAME}_subs_node
	DESTINATION lib/${PROJECT_NAME}
)

ament_package()
