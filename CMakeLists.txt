cmake_minimum_required (VERSION 3.0)

PROJECT(segmentation)

#Set the compiler
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_BUILD_TYPE Release)
set( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set( LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

IF(EXISTS ${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    conan_basic_setup()
ENDIF()

# Requires OpenCV
FIND_PACKAGE( OpenCV 4.0.0 REQUIRED )
MESSAGE("OpenCV version : ${OpenCV_VERSION}")

include_directories(${OpenCV_INCLUDE_DIRS} include)
link_directories(${OpenCV_LIB_DIR})

ADD_EXECUTABLE( ${PROJECT_NAME} ${PROJECT_SOURCE_DIR}/src/demo/main.cpp ${PROJECT_SOURCE_DIR}/src/utils/MultipleImageWindow.cpp)
TARGET_LINK_LIBRARIES( ${PROJECT_NAME} ${OpenCV_LIBS} )
