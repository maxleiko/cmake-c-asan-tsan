# This CMake configuration will need you to have pre-installed libraries:
#  - asan
#  - tsan
#  - ubsan
# 
# On a recent Debian:
#   sudo apt install libubsan1 libtsan0 libasan5
cmake_minimum_required (VERSION 3.0)
project(my-project C)
set(CMAKE_C_STANDARD 11)
add_compile_options(-Wall -Wextra -Wpedantic)
set(CMAKE_CXX_FLAGS_DEBUG_INIT -g -O1)

# Your program sources
set(SOURCES src/main.c)

# Default build type: "Debug"
if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Debug")
endif ()

# What to do if in "Debug" build type
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
  add_executable(${PROJECT_NAME}-asan ${SOURCES})
  target_compile_options(${PROJECT_NAME}-asan PUBLIC -fsanitize=address -fsanitize=undefined)
  target_link_libraries(${PROJECT_NAME}-asan -lasan -lubsan ${CMAKE_THREAD_LIBS_INIT})

  add_executable(${PROJECT_NAME}-tsan ${SOURCES})
  target_compile_options(${PROJECT_NAME}-tsan PUBLIC -fsanitize=thread -fsanitize=undefined)
  target_link_libraries(${PROJECT_NAME}-tsan -ltsan -lubsan ${CMAKE_THREAD_LIBS_INIT})
endif()

# What to do if in "Release" build type
if(CMAKE_BUILD_TYPE STREQUAL "Release")
  add_executable(${PROJECT_NAME} ${SOURCES})
  target_link_libraries(${PROJECT_NAME} ${CMAKE_THREAD_LIBS_INIT})
endif()
