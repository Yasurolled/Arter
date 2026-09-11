cmake_minimum_required(VERSION 3.16)
project(arter C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

find_package(raylib 4.0 REQUIRED)
find_path(RAYGUI_INCLUDE_DIR raygui.h)

if(NOT RAYGUI_INCLUDE_DIR)
  message(FATAL_ERROR "raygui.h was not found. Install raygui or add its directory with -DRAYGUI_INCLUDE_DIR=/path/to/raygui")
endif()

add_executable(arter arter.c)
target_include_directories(arter PRIVATE ${RAYGUI_INCLUDE_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(arter PRIVATE raylib)

if(APPLE)
  target_link_libraries(arter PRIVATE "-framework IOKit" "-framework Cocoa" "-framework OpenGL")
elseif(UNIX AND NOT APPLE)
  target_link_libraries(arter PRIVATE m pthread dl rt X11)
endif()

if(WIN32)
  target_link_libraries(arter PRIVATE winmm)
  set_target_properties(arter PROPERTIES WIN32_EXECUTABLE TRUE)
endif()
