
cmake_minimum_required( VERSION 3.2 ) 
set( CMAKE_CONFIGURATION_TYPES "Debug;Release" CACHE STRING "Supported configuration types" FORCE )
        
project( hopscotch-map-adapter LANGUAGES CXX )
get_directory_property( is_subproject PARENT_DIRECTORY )
include( CMakeDependentOption REQUIRED )

if ( NOT GIT_EXECUTABLE )
    find_package( Git )
    if ( NOT GIT_FOUND )
        message( FATAL_ERROR "git installation was not found." )
    endif()
endif()

execute_process(
    COMMAND ${GIT_EXECUTABLE} rev-parse --abbrev-ref HEAD
    WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
    OUTPUT_VARIABLE GIT_BRANCH
    OUTPUT_STRIP_TRAILING_WHITESPACE
)
execute_process(
    COMMAND ${GIT_EXECUTABLE} rev-parse HEAD
    WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
    OUTPUT_VARIABLE GIT_HASH
    OUTPUT_STRIP_TRAILING_WHITESPACE
) 

message( STATUS "" )
message( STATUS "-----------------------------------------------------------" )
message( STATUS "" )
message( STATUS "hopscotch-map-adapter" )
message( STATUS "Git current branch: ${GIT_BRANCH}" )
message( STATUS "Git commit hash: ${GIT_HASH}" )
message( STATUS "" )
message( STATUS "-----------------------------------------------------------" )

add_library( hopscotch-map-adapter INTERFACE )
target_include_directories( hopscotch-map-adapter INTERFACE src/src )
target_sources( hopscotch-map-adapter INTERFACE
                "${CMAKE_CURRENT_SOURCE_DIR}/src/src/hopscotch_hash.h"
                "${CMAKE_CURRENT_SOURCE_DIR}/src/src/hopscotch_map.h"
                "${CMAKE_CURRENT_SOURCE_DIR}/src/src/hopscotch_sc_map.h"
                "${CMAKE_CURRENT_SOURCE_DIR}/src/src/hopscotch_sc_set.h"
                "${CMAKE_CURRENT_SOURCE_DIR}/src/src/hopscotch_set.h" )
