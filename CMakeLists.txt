cmake_minimum_required(VERSION 3.15)
project(read_nrrd)

set(CMAKE_CXX_STANDARD 17)
find_package(OpenCV REQUIRED)
find_package(Boost REQUIRED COMPONENTS system iostreams)
include_directories(${OpenCV_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})
add_executable(read_nrrd read_nrrd.cpp)
target_link_libraries(read_nrrd ${OpenCV_LIBS} ${Boost_LIBRARIES})