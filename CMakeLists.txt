cmake_minimum_required(VERSION 3.14)
project(libshell)

set (CMAKE_CXX_STANDARD 14)
set(MSVC_RUNTIME "dynamic")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

# Only build libshell library when included as subdirectory
find_package(Eigen3 3.3 REQUIRED NO_MODULE)

# Add your project files
if(MSVC)
	add_definitions(-DEIGEN_STRONG_INLINE=inline)
	add_compile_options(/bigobj)
endif()

file(GLOB LIBFILES src/*.cpp src/SecondFundamentalForm/*.cpp src/MaterialModel/*.cpp)
add_library(${PROJECT_NAME} STATIC ${LIBFILES})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_link_libraries(${PROJECT_NAME} PUBLIC Eigen3::Eigen)
