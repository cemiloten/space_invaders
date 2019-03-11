cmake_minimum_required(VERSION 3.1)
project(space_invaders)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

link_directories(${CMAKE_SOURCE_DIR}/lib)

file(GLOB_RECURSE SOURCE_FILES
    ${CMAKE_SOURCE_DIR}/src/*.c
    ${CMAKE_SOURCE_DIR}/src/*.cpp)

file(GLOB_RECURSE HEADER_FILES
    ${CMAKE_SOURCE_DIR}/src/*.h
    ${CMAKE_SOURCE_DIR}/src/*.hpp)

add_executable(${PROJECT_NAME} ${SOURCE_FILES} ${HEADER_FILES})

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

# Look for packages
find_package(OpenGL REQUIRED)
find_package(GLFW3 REQUIRED)
message(STATUS "Found GLFW3 in ${GLFW3_INCLUDE_DIR}")

add_library(GLAD "thirdparty/glad.c")

# Have all libraries in one variable
set(LIBS glfw3 opengl32 GLAD)

include_directories(
    "${CMAKE_SOURCE_DIR}/src"
    "${CMAKE_SOURCE_DIR}/include"
)

target_link_libraries(${PROJECT_NAME} ${LIBS})

# Copy dlls
if(WIN32)
	add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
		COMMAND ${CMAKE_COMMAND} -E copy_directory
		"${PROJECT_SOURCE_DIR}/dlls"
		$<TARGET_FILE_DIR:${PROJECT_NAME}>)
endif()