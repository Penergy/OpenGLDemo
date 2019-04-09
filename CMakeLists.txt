cmake_minimum_required(VERSION 2.8)
project(openGLUtahTeePot)

# turn off the optimazation under Debug configuration
if (CMAKE_CXX_COMPILER_ID MATCHES GNU)
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0")
    set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O0")
endif()

set(OPENGL_INCLUDE_DIRS "../dependencies/include/GL")
set(OPENGL_LIBRARIES_WIN "./dependencies/win64/libopengl.lib")
set(OPENGL_LIBRARIES_LIN "../dependencies/linux64/libopengl.so")

set(GLUT_INCLUDE_DIRS "./dependencies/include/GL")
set(GLUT_LIBRARIES_WIN "./dependencies/win64/libglut.lib")
set(GLUT_LIBRARIES_LIN "../dependencies/linux64/libglut.so")

if(MSVC)
  # Force to always compile with W4
  if(CMAKE_CXX_FLAGS MATCHES "/W[0-4]")
    string(REGEX REPLACE "/W[0-4]" "/W4" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
  else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
  endif()
elseif(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX)
  # Update if necessary
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wno-long-long -pedantic")
endif()

add_executable(openGLUtahTeePot main.cpp)

target_include_directories(
    openGLUtahTeePot 
    PRIVATE ${CMAKE_CURRENT_LIST_DIR}/dependencies/includes/GL
)

if(WIN32)
    if(CMAKE_BUILD_TYPE MATCHES Debug)
        target_link_libraries(
            openGLUtahTeePot 
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/win64/glut.lib
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/win64/OpenGL32.Lib 
        )
    elseif(CMAKE_BUILD_TYPE MATCHES Release)
        target_link_libraries(
            openGLUtahTeePot 
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/win64/glut.lib
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/win64/OpenGL32.Lib
        )
    endif()
elseif(UNIX)
    target_compile_options(openGLUtahTeePot PRIVATE -std=c++11 -g)
    if(CMAKE_BUILD_TYPE MATCHES Debug)
        message(STATUS "Linux debug")
        target_link_libraries(
            openGLUtahTeePot
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/linux64/libglut.so
            #${CMAKE_CURRENT_LIST_DIR}/dependencies/linux64/libopengl.so
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/linux64/libGL.so
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/linux64/libGLU.so

        )
    elseif(CMAKE_BUILD_TYPE MATCHES Release)
        message(STATUS "Linux release")
        target_link_libraries(
            openGLUtahTeePot
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/linux64/libglut.so
            #${CMAKE_CURRENT_LIST_DIR}/dependencies/linux64/libopengl.so
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/linux64/libGL.so
            ${CMAKE_CURRENT_LIST_DIR}/dependencies/linux64/libGLU.so
        )
    endif()
    set_target_properties(openGLUtahTeePot
                          PROPERTIES OUTPUT_NAME openGLUtahTeePot
                          INSTALL_RPATH "$ORIGIN"
                          BUILD_WITH_INSTALL_RPATH TRUE)
endif()
