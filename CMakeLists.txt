cmake_minimum_required(VERSION 3.13)
project(openGLUtahTeePot)

set(CMAKE_CXX_STANDARD 11)
#set(OPENGL_INCLUDE_DIRS "/usr/local/include/GL")
#set(OPENGL_LIBRARIES "/usr/local/lib/libpangolin.so")
#set(GLUT_INCLUDE_DIRS "/usr/local/include/GL")
#set(GLUT_LIBRARIES "/usr/lib/x86_64-linux-gnu/libglut.so")

# 添加Pangolin依赖
find_package( GLUT )
include_directories( ${GLUT_INCLUDE_DIRS} )

find_package(OpenGL REQUIRED)
include_directories( ${OPENGL_INCLUDE_DIRS} )

add_executable(openGLUtahTeePot main.cpp)

target_link_libraries( openGLUtahTeePot ${OPENGL_LIBRARIES} )
target_link_libraries( openGLUtahTeePot ${GLUT_LIBRARIES} )