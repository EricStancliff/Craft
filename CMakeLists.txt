cmake_minimum_required(VERSION 2.8)

project(craft LANGUAGES C)

FILE(GLOB SOURCE_FILES src/*.c)

add_executable(
    craft
    ${SOURCE_FILES}
    deps/lodepng/lodepng.c
    deps/noise/noise.c
    deps/sqlite/sqlite3.c
    deps/tinycthread/tinycthread.c)


add_subdirectory(deps/glfw)
include_directories(deps/gl3w)
include_directories(deps/lodepng)
include_directories(deps/noise)
include_directories(deps/sqlite)
include_directories(deps/tinycthread)

if(APPLE)
    add_definitions(-std=c99 -O3)
    target_link_libraries(craft glfw
        ${GLFW_LIBRARIES} ${CURL_LIBRARIES})
endif()

if(UNIX)
    add_definitions(-std=c99 -O3)

    target_link_libraries(craft dl glfw
        ${GLFW_LIBRARIES} ${CURL_LIBRARIES})
endif()

