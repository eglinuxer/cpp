cmake_minimum_required(VERSION 3.24 FATAL_ERROR)

project(cpp
    VERSION 0.0.1
    DESCRIPTION "eglinux cpp study"
    HOMEPAGE_URL "https://github.com/eglinuxer/cpp"
    LANGUAGES CXX
)

string(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_MESSAGE_CONTEXT cpp)


