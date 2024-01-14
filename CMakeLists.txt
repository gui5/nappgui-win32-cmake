cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

# create project
project(hellonapp LANGUAGES C CXX)

# add dependencies
include(cmake/CPM.cmake)

CPMAddPackage(
  NAME nappgui
  VERSION 1.4.0
  GITHUB_REPOSITORY frang75/nappgui_src
  OPTIONS "NAPPGUI_DEMO NO"
)


find_package(nappgui REQUIRED)
include_directories(${nappgui_SOURCE_DIR}/src/)
file(GLOB NAPPGUI_LIBS ${CMAKE_BINARY_DIR}/Debug/lib/*.lib)
# add executable
set(WIN32_EXECUTABLE TRUE)
add_executable(hellonapp WIN32 src/main.cpp)
# do not blur
target_sources(hellonapp PRIVATE src/dpi-aware.manifest)
target_link_libraries(hellonapp ${NAPPGUI_LIBS} )





