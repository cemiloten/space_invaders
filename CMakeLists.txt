cmake_minimum_required(VERSION 3.1)
set(CMAKE_CXX_STANDARD 17)

project(space_invaders)

# For YouCompleteMe (Vim) autocompletion
# set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include_directories(
    /usr/local/include
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

set(LIBRARIES_DIR "/usr/local/lib")
link_directories(${LIBRARIES_DIR})

find_library(LIB_GLFW3    NAMES glfw.3    PATHS ${LIBRARIES_DIR})

file(GLOB SOURCE_FILES "source/*")
file(GLOB HEADER_FILES "include/space_invaders/*")
add_executable(space_invaders
    ${SOURCE_FILES}
    ${HEADER_FILES})

target_link_libraries(space_invaders
    "-framework CoreVideo"
    "-framework IOKit"
    "-framework Cocoa"
    "-framework OpenGL"
    ${LIB_GLFW3}
)
