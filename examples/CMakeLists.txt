cmake_minimum_required(VERSION 3.1)
project(example)

IF(UNIX)
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -pthread")
ELSE(UNIX)
    set(CMAKE_CXX_STANDARD 14)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    set(CMAKE_CXX_EXTENSIONS ON)
ENDIF(UNIX)

SET(ENABLE_SSL OFF)
SET(ENABLE_JAVA OFF)

if (ENABLE_SSL)
    add_definitions(-DCINATRA_ENABLE_SSL)
    message(STATUS "Use SSL")
    find_package(Boost COMPONENTS system filesystem REQUIRED)
endif()

if (ENABLE_JAVA)
    find_package(JNI REQUIRED)
    message(STATUS "Use Java")
endif()

include_directories(
        "/usr/local/include"
        "../include"
        "../thirdparty/msgpack-c/include"
        "../thirdparty/asio")

add_executable(basic_server server/main.cpp)
add_executable(basic_client client/main.cpp)

if (ENABLE_SSL)
    target_link_libraries(basic_server ${Boost_LIBRARIES} -lssl -lcrypto -lpthread)
    target_link_libraries(basic_client ${Boost_LIBRARIES} -lssl -lcrypto -lpthread)
else()
    target_link_libraries(basic_server ${Boost_LIBRARIES})
    target_link_libraries(basic_client ${Boost_LIBRARIES})
endif()
