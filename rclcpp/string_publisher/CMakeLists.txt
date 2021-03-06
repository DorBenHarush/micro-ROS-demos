cmake_minimum_required(VERSION 3.5)

project(string_publisher LANGUAGES CXX)

find_program(CLANG_TIDY clang-tidy)
if(CLANG_TIDY)
  set(CMAKE_CXX_CLANG_TIDY clang-tidy -checks=*)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp QUIET)
find_package(std_msgs REQUIRED)


# Do not compile package if rclcpp is not found
if (NOT rclcpp_FOUND)
  message(WARNING "${PROJECT_NAME} will be ignored due to rclcpp is not installed")
  return()
endif()


add_executable(${PROJECT_NAME} main.cpp)
ament_target_dependencies(${PROJECT_NAME} rclcpp std_msgs)

install(
  TARGETS
    ${PROJECT_NAME}
  DESTINATION
    ${PROJECT_NAME}
  )

