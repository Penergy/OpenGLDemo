cmake_minimum_required(VERSION 2.8)
project(openGLUtahTeePot)

set(CMAKE_CXX_STANDARD 11)

set(OPENGL_INCLUDE_DIRS "../dependencies/include/GL")
set(OPENGL_LIBRARIES_WIN "./dependencies/win64/libopengl.lib")
set(OPENGL_LIBRARIES_LIN "../dependencies/linux64/libopengl.so")

set(GLUT_INCLUDE_DIRS "./dependencies/include/GL")
set(GLUT_LIBRARIES_WIN "./dependencies/win64/libglut.lib")
set(GLUT_LIBRARIES_LIN "../dependencies/linux64/libglut.so")

if(WIN32)
    message(STATUS "message to windows")
    set(GLUT_INCLUDE_DIR "..\\include\\GL")
elseif(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX)
    # Update if necessary
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wno-long-long -pedantic")
endif()

# Input GLUT && OpenGL
find_package( GLUT )
if(WIN32)
    include_directories( ${GLUT_INCLUDE_DIR} )
else()
    include_directories( ${GLUT_INCLUDE_DIRS} )
endif()

find_package(OpenGL REQUIRED)
include_directories( ${OPENGL_INCLUDE_DIRS} )

add_executable(openGLUtahTeePot main.cpp)

target_include_directories(
    openGLUtahTeePot 
    PRIVATE ./dependencies/includes/GL
)

if(WIN32)
    target_link_libraries( openGLUtahTeePot ${OPENGL_LIBRARIES_WIN} )
    target_link_libraries( openGLUtahTeePot ${GLUT_LIBRARIES_WIN} )
else()
    target_link_libraries( openGLUtahTeePot ${OPENGL_LIBRARIES_LIN} )
    target_link_libraries( openGLUtahTeePot ${GLUT_LIBRARIES_LIN} )
endif()

