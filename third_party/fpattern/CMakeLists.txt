include(FetchContent)

FetchContent_Declare(fpattern
    GIT_REPOSITORY "https://github.com/Loadmaster/fpattern"
    GIT_TAG "v1.9"
)

FetchContent_GetProperties(fpattern)
if (NOT fpattern_POPULATED)
    FetchContent_Populate(fpattern)
endif()

if(MSVC)
    set(CMAKE_DEBUG_POSTFIX "d")
endif()

add_library(fpattern2 STATIC
    "${fpattern_SOURCE_DIR}/debug.h"
    "${fpattern_SOURCE_DIR}/fpattern.c"
    "${fpattern_SOURCE_DIR}/fpattern.h"
)

if(NOT WIN32)
    target_compile_definitions(fpattern2 PRIVATE
        "-Dunix"
    )
endif()

set(FPATTERN_LIBRARY "fpattern2" PARENT_SCOPE)
set(FPATTERN_INCLUDE_DIR "${fpattern_SOURCE_DIR}" PARENT_SCOPE)
