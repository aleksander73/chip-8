cmake_minimum_required(VERSION 3.29.2)
project(chip-8)

set(CMAKE_CXX_STANDARD 20)
set(SRC_FILES "")

file(GLOB_RECURSE SRC_FILES "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")

add_executable(chip-8
    ${SRC_FILES}
)

target_include_directories(chip-8 PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/include"
)

target_link_libraries(chip-8 PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/libs/SDL3.dll"
)

add_custom_command(TARGET chip-8 POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different "${CMAKE_CURRENT_SOURCE_DIR}/libs/SDL3.dll" $<TARGET_FILE_DIR:chip-8>)
