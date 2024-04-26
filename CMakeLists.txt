cmake_minimum_required(VERSION 3.8)
project(graph_ros2_tests)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

set(CMAKE_BUILD_TYPE Debug)

# find dependencies
find_package(ament_cmake REQUIRED)

find_package(graph_ros2 REQUIRED)
find_package(graph_display REQUIRED)

add_executable(test_solver src/${PROJECT_NAME}/test_solver.cpp)
ament_target_dependencies(test_solver
  PUBLIC
    graph_ros2
    graph_display
)
target_include_directories(test_solver
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include/${PROJECT_NAME}>)

install(TARGETS test_solver
  DESTINATION lib/${PROJECT_NAME})

#install(DIRECTORY launch config
#  DESTINATION share/${PROJECT_NAME} )

##########################################

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
