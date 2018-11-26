cmake_minimum_required(VERSION 3.0)
project(Lighting)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_INSTALL_RPATH "./lib")
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/bin)

find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)

include(FindPkgConfig)
pkg_search_module(GLFW REQUIRED glfw3)
pkg_search_module(glm REQUIRED glm)

file(GLOB_RECURSE SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)

set(INCLUDES
  ${CMAKE_CURRENT_SOURCE_DIR}/include/
  ${CMAKE_CURRENT_SOURCE_DIR}/include/vendor/
  ${OPENGL_INCLUDE_DIR}
  ${GLEW_INCLUDE_DIR}
  ${GLFW_INCLUDE_DIR}
  ${GLM_INCLUDE_DIR})

set(LIBRARIES
  ${OPENGL_LIBRARIES}
  ${GLEW_LIBRARIES}
  ${GLFW_STATIC_LIBRARIES})

add_executable(Lighting ${SOURCES})
target_include_directories(Lighting PUBLIC ${INCLUDES})
target_link_libraries(Lighting ${LIBRARIES})
if(${CMAKE_CXX_COMPILER_ID} STREQUAL GNU)
  target_compile_options(Lighting PUBLIC -Wall -pedantic)
endif()
