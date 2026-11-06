cmake_minimum_required(VERSION 4.3)
project(VulkanTest)

set(CMAKE_CXX_STANDARD 23)

find_package(Vulkan REQUIRED)
find_package(glfw3 CONFIG)
find_package(glm CONFIG)

message(STATUS "Vulkan include: ${Vulkan_INCLUDE_DIRS}")
message(STATUS "Vulkan lib:     ${Vulkan_LIBRARIES}")
message(STATUS "Found:          ${Vulkan_FOUND}")

if (glfw3_FOUND)
    message(STATUS "GLFW found via package config in: ${glfw3_DIR}")
endif()

if (NOT glfw3_FOUND)
    include(FetchContent)
    FetchContent_Declare(glfw
            GIT_REPOSITORY https://github.com/glfw/glfw.git
            GIT_TAG        3.4)
    set(GLFW_BUILD_DOCS     OFF CACHE BOOL "" FORCE)
    set(GLFW_BUILD_TESTS    OFF CACHE BOOL "" FORCE)
    set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
    FetchContent_MakeAvailable(glfw)
endif()

if (glm_FOUND)
    message(STATUS "GLM found via package config in: ${glm_DIR}")
endif()

if (NOT glm_FOUND)
    include(FetchContent)
    FetchContent_Declare(glm
            GIT_REPOSITORY https://github.com/g-truc/glm.git
            GIT_TAG        1.0.1)
    FetchContent_MakeAvailable(glm)
endif()

add_executable(VulkanTest main.cpp)

target_link_libraries(VulkanTest PRIVATE glfw Vulkan::Vulkan glm::glm)
