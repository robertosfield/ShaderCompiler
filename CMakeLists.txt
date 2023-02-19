cmake_minimum_required(VERSION 3.7)

project(ShaderCompiler
    VERSION 0.0.0
    DESCRIPTION "ShaderCompiler library that builds a single library from glslang source."
    LANGUAGES CXX
)
set(VSGIMGUI_SOVERSION 0)
SET(VSGIMGUI_RELEASE_CANDIDATE 0)

set(VSGIMGUI_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}" CACHE INTERNAL "Root source directory of ShaderCompiler")
set(VSGIMGUI_BINARY_DIR "${CMAKE_CURRENT_BINARY_DIR}" CACHE INTERNAL "Root binary directory of ShaderCompiler")

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)


if ((NOT EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/glslang/CMakeLists.txt))
    find_package(Git QUIET)

    execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                    RESULT_VARIABLE GIT_SUBMOD_RESULT)

    if(NOT GIT_SUBMOD_RESULT EQUAL "0")
        message(FATAL_ERROR "git submodule update --init --recursive failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
    endif()
endif()

# source directory for main ShaderCompiler library
# add_subdirectory(glslang)

include(build_vars.cmake)


