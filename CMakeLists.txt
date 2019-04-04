cmake_minimum_required(VERSION 2.8)
project(openGLUtahTeePot)

set(CMAKE_CXX_STANDARD 11)
#set(OPENGL_INCLUDE_DIRS "/usr/local/include/GL")
#set(OPENGL_LIBRARIES "/usr/local/lib/libpangolin.so")
#set(GLUT_INCLUDE_DIRS "/usr/local/include/GL")
#set(GLUT_LIBRARIES "/usr/lib/x86_64-linux-gnu/libglut.so")

if(WIN32)
    message(STATUS "message to windows")
    set(GLUT_INCLUDE_DIR "..\\include\\GL")
elseif(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX)
    # Update if necessary
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wno-long-long -pedantic")
endif()

# ÃÌº”GLUT“¿¿µ
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
    PRIVATE ../includes/GL
)

target_link_libraries( openGLUtahTeePot ${OPENGL_LIBRARIES} )
target_link_libraries( openGLUtahTeePot ${GLUT_LIBRARIES} )