cmake_minimum_required(VERSION 3.8)

project(rest_rpc)

LIST(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
INCLUDE(cmake/ModuleImport.cmake)
INCLUDE(cmake/ModuleCompileOptions.cmake)

IF (WIN32)
    LINK_DIRECTORIES(${CMAKE_SOURCE_DIR}/bin)
    SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin)
    SET(LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin)
ELSE(WIN32)
    LINK_DIRECTORIES(${CMAKE_SOURCE_DIR}/bin/${CMAKE_BUILD_TYPE})
    SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin/${CMAKE_BUILD_TYPE})
    SET(LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin/${CMAKE_BUILD_TYPE})
ENDIF(WIN32)

add_subdirectory(examples)
