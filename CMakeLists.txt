cmake_minimum_required(VERSION 2.8)
project(boost-endian)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
include(ExternalProject)

ExternalProject_Add(endian
  GIT_REPOSITORY "https://github.com/Beman/endian.git"
  GIT_TAG master
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  INSTALL_COMMAND ""
  TEST_COMMAND "")

include ( CMakePackageConfigHelpers )

set (${PROJECT_NAME}_INCLUDE_DIRS "${CMAKE_CURRENT_BINARY_DIR}/endian-prefix/src/endian/include")

#### Install headers
set(header_install_dir "include/${PROJECT_NAME}")
install(DIRECTORY "${${PROJECT_NAME}_INCLUDE_DIRS}" DESTINATION "${header_install_dir}")

#### Generate CMake modules for importing this package
include(jbms-WriteConfig)
write_config_file(
  TEMPLATE "${CMAKE_CURRENT_SOURCE_DIR}/cmake/config.cmake.in"
  PATH_VARS ${PROJECT_NAME}_INCLUDE_DIRS
  REL_PATH "${header_install_dir}" )
