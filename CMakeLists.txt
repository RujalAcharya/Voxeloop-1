include(FetchContent)
cmake_minimum_required(VERSION 3.17)
project(voxeloop)

set(CMAKE_CXX_STANDARD 17)
set(CURRENT_COMPILER clang++)
set(BUILD_SHARED_LIBS OFF)

if(MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
else()
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}") # -Wall -Wextra -Wpedantic")
  if(NOT WIN32)
    set(GLAD_LIBRARIES dl)
  endif()
endif()

FetchContent_Declare(
  voxeloop-base
  GIT_REPOSITORY https://github.com/RujalAcharya/voxeloop-base.git
  # GIT_REPOSITORY https://github.com/jarp0l/voxeloop-base.git
  GIT_TAG main)

FetchContent_MakeAvailable(voxeloop-base)

include_directories(core/include)
include_directories(core/include/Data\ Structures)

file(GLOB PROJECT_HEADERS core/include/*.hpp)
file(GLOB PROJECT_HEADERS core/include/Data\ Structures/*.hpp)
file(GLOB PROJECT_SOURCES core/src/*.cpp)

source_group("Headers" FILES ${PROJECT_HEADERS})
source_group("Sources" FILES ${PROJECT_SOURCES})

add_executable(${PROJECT_NAME} ${PROJECT_HEADERS} ${PROJECT_SOURCES})

target_link_libraries(${PROJECT_NAME} glad glm imgui stb miniaudio)
