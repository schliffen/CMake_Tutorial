# set minimum cmake version
cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

# project name and language
project(recipe-03_1 LANGUAGES CXX)

# generate a library from sources
add_library(message-obj
  OBJECT
    Message.hpp
    Message.cpp
  )

#
set_target_properties(message-obj 
    PROPERTIES
    POSITION_INDEPENDENT_CODE 1
)

add_library(message-so
SHARED 
$<TARGET_OBJECTS:message-obj>
)
set_target_properties(message-so
PROPERTIES
OUTPUT_NAME "message"
)

add_library(message-st
STATIC 
$<TARGET_OBJECTS:message-obj>
)
set_target_properties(message-st
PROPERTIES
OUTPUT_NAME "message"
)

add_executable(hello-obj hello-world.cpp)

target_link_libraries(hello-obj message-obj message-st message-so)
