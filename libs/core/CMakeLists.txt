
set(target core)
message(STATUS "lib ${target}")

configure_file(meta.template meta.h)

set(SOURCES

    declspec.h

    aabb.h
    aabb.cpp
    abstractapplication.h
    abstractapplication.cpp
    datacore/abstractdata.h
    datacore/abstractdata.cpp
    abstracttimer.h
    bufferobject.h
    bufferobject.cpp
    camera.h
    camera.cpp
    chronotimer.h
    chronotimer.cpp
    common.h
    fileassociatedshader.h
    fileassociatedshader.cpp
    framebufferobject.h
    framebufferobject.cpp
    glformat.h
    glformat.cpp
    gpuquery.h
    gpuquery.cpp
    group.h
    group.cpp
    messagehandler.h
    messagehandler.cpp
    mathmacros.h
    node.h
    node.cpp
    objio.h
    objio.cpp
    polygonaldrawable.h
    polygonaldrawable.cpp
    polygonalgeometry.h
    polygonalgeometry.cpp
    program.h
    program.cpp
    screenquad.h
    screenquad.cpp
    shader.h
    shader.cpp
    timer.h
    timer.cpp
)

source_group_by_path(${CMAKE_CURRENT_SOURCE_DIR} "\\\\.cpp$|\\\\.c$|\\\\.h$|\\\\.hpp$|\\\\.ui$" 
    ${CGSEE_SOURCE_GROUP} ${SOURCES})

# setup target

include_directories(
    ${CMAKE_CURRENT_BINARY_DIR})

add_library(${target} SHARED ${HEADERS} ${SOURCES})

qt5_use_modules(${target} Widgets OpenGL)

target_link_libraries(${target}
    ${OPENGL_LIBRARIES}
    ${GLEW_LIBRARY}
)


set_target_properties(${target}
    PROPERTIES
    LINKER_LANGUAGE CXX
    COMPILE_DEFINITIONS_DEBUG   "${DEFAULT_COMPILE_DEFS_DEBUG}"
    COMPILE_DEFINITIONS_RELEASE "${DEFAULT_COMPILE_DEFS_RELEASE}"
    COMPILE_FLAGS               "${DEFAULT_COMPILE_FLAGS}"
    LINK_FLAGS_DEBUG            "${DEFAULT_LINKER_FLAGS_DEBUG}"
    LINK_FLAGS_RELEASE          "${DEFAULT_LINKER_FLAGS_RELEASE}"
    FOLDER ${CGSEE_LIB_FOLDER}
    DEBUG_POSTFIX "d${DEBUG_POSTFIX}")

add_definitions("-DCGSEE_EXPORTS")
