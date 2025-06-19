cmake_minimum_required(VERSION 3.12)

project(obj)

add_library(obj obj.c)

add_subdirectory(deps/array)

target_link_libraries(obj PRIVATE array)
target_include_directories(obj PUBLIC "${obj_SOURCE_DIR}")
