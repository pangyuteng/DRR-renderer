project(DRRgenerator)
cmake_minimum_required(VERSION 2.8)
ADD_DEFINITIONS(
    -std=c++11
    -O3
)
message("CMAKE_BUILD_TYPE is ${CMAKE_BUILD_TYPE}")
find_package(OpenMP)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()
find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_INCLUDE_DIRS} )

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")
find_package( Eigen3 REQUIRED )
include_directories( ${EIGEN3_INCLUDE_DIR} )

message(STATUS "===================")
message(STATUS ${OpenCV_FOUND})
message(STATUS ${OpenCV_INCLUDE_DIRS})
message(STATUS ${Eigen3_FOUND})
message(STATUS ${EIGEN3_INCLUDE_DIR})

add_executable(${PROJECT_NAME} main.cpp DRRgenerator.cpp )
target_link_libraries( ${PROJECT_NAME} ${OpenCV_LIBS})

install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
