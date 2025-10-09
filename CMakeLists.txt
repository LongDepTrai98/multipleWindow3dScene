cmake_minimum_required(VERSION 3.12)
include(FetchContent)
set(CMAKE_TOOLCHAIN_FILE "./vcpkg/scripts/buildsystems/vcpkg.cmake" CACHE STRING "Vcpkg toolchain file")
project(multipleWindow3dScene)
# Enable solution folders in Visual Studio and Folders in Xcode
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
# Point CMake where to look for module files.
list(APPEND CMAKE_MODULE_PATH ${IMGUI_NODE_EDITOR_ROOT_DIR}/misc/cmake-modules)
# Node editor use C++20
set(CMAKE_CXX_STANDARD            20)
set(CMAKE_CXX_STANDARD_REQUIRED   YES)
set(project_name app)

#add threepp lib
set(THREEPP_BUILD_TESTS OFF)
set(THREEPP_BUILD_EXAMPLES OFF)
set(THREEPP_WITH_GLFW OFF) 
FetchContent_Declare(
        threepp
        GIT_REPOSITORY https://github.com/markaren/threepp.git
)
FetchContent_MakeAvailable(threepp)
set_target_properties(threepp PROPERTIES FOLDER "backend")
#

#find glfw3
find_package(OpenGL REQUIRED)
find_package(glfw3 CONFIG REQUIRED)



add_executable(${project_name} ./src/main.cpp)
target_link_libraries(${project_name} PRIVATE
	glfw
    threepp::threepp)