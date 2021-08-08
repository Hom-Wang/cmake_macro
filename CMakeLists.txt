cmake_minimum_required(VERSION 3.0.0)
project(exmaple VERSION 0.1.0)
message("CMAKE_PROJECT_NAME = ${CMAKE_PROJECT_NAME}")

# utility.cmake
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR})
include(Utility)

set(COMMIT_HASH "")
set(COMMIT_DATE "")
get_last_commit_hash(COMMIT_HASH)
get_last_commit_date(COMMIT_DATE)
message(STATUS "commit: ${COMMIT_HASH}, date: ${COMMIT_DATE}")


set(PROJECT_PATH ${CMAKE_SOURCE_DIR})
set(TARGET_NAME ${CMAKE_PROJECT_NAME})

file(GLOB ALL_INCLUDE "inc")

link_libraries(m)
add_executable(${TARGET_NAME}
    main.c
)

add_definitions(
    -DCOMMIT_HASH=${COMMIT_HASH}
    -DCOMMIT_DATE=${COMMIT_DATE}
)

include_directories(
    ${ALL_INCLUDE}
)
set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})

add_custom_target(run
    COMMAND ${TARGET_NAME}
)

set_target_properties(${TARGET_NAME} PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${PROJECT_PATH}/build"
)
