cmake_minimum_required(VERSION 3.19)

project(dpp-static-build VERSION 1.0 DESCRIPTION "DPP static build test")

set(BUILD_SHARED_LIBS OFF)

# Set library options
set(DPP_INSTALL OFF)
set(DPP_BUILD_TEST OFF)
set(DPP_NO_VCPKG ON)

# Libraries
include(FetchContent)

FetchContent_Declare(DPP GIT_REPOSITORY "https://github.com/brainboxdotcc/DPP.git" 
    GIT_TAG "ebdf0bd198ef046778e87ee709c852b50bb6632b" OVERRIDE_FIND_PACKAGE)

FetchContent_MakeAvailable(DPP)

# Ensure packages are installed
find_package(dpp REQUIRED)

# Create an executable
add_executable(${PROJECT_NAME}
    src/main.cpp
)

# Linking libraries
target_link_libraries(${PROJECT_NAME}
    zstd
    dpp
    opus
    opusfile
    ogg
)
 
# Specify includes
target_include_directories(${PROJECT_NAME} PRIVATE
    /usr/include/opus
)

# Set C++ version
set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 20
    CXX_STANDARD_REQUIRED ON
)
