cmake_minimum_required(VERSION 3.5)
project(fusion_pkg)

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
find_package(ament_cmake_python REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclpy REQUIRED)
find_package(std_msgs REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

include_directories(include)

add_executable(${PROJECT_NAME}_pubcpp_node src/fusion_pubcpp_node.cpp)
ament_target_dependencies(${PROJECT_NAME}_pubcpp_node rclcpp)

add_executable(${PROJECT_NAME}_subcpp_node src/fusion_subcpp_node.cpp)
ament_target_dependencies(${PROJECT_NAME}_subcpp_node rclcpp)

# Install C++ executables
install(TARGETS
	${PROJECT_NAME}_pubcpp_node
	${PROJECT_NAME}_subcpp_node
	DESTINATION lib/${PROJECT_NAME}
)

# Install Python executables
install(PROGRAMS
	scripts/fusion_pubpy_node.py
	scripts/fusion_subpy_node.py
	DESTINATION lib/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
