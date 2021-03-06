cmake_minimum_required(VERSION 3.10)
project(vk LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 20)

option(GLFW_BUILD_DOCS OFF)
option(GLFW_BUILD_TESTS OFF)
option(GLFW_BUILD_EXAMPLES OFF)
option(GLFW_BUILD_TESTS OFF)
option(GLFW_INSTALL OFF)
option(ENABLE_HLSL OFF)

add_subdirectory(external/glfw)
add_subdirectory(external/glslang)
add_subdirectory(external/SPIRV-Cross)

add_library(imgui STATIC 
    external/imgui/backends/imgui_impl_glfw.cpp
    external/imgui/backends/imgui_impl_vulkan.cpp
    external/imgui/imgui_demo.cpp
    external/imgui/imgui_draw.cpp
    external/imgui/imgui_tables.cpp
    external/imgui/imgui.cpp
    external/imgui/imgui_widgets.cpp
    external/imgui-vulkan-hpp-backend/imgui_impl_vulkan_hpp.cpp
)
target_include_directories(
    imgui PUBLIC
    "${PROJECT_SOURCE_DIR}/external/vulkan/include"
    "${PROJECT_SOURCE_DIR}/external/imgui"
    "${PROJECT_SOURCE_DIR}/external/imgui/backends"
    "${PROJECT_SOURCE_DIR}/external/imgui-vulkan-hpp-backend"
)

file(GLOB sources source/*.cpp)
add_executable(${PROJECT_NAME} 
    ${sources}
)

target_link_libraries(
    ${PROJECT_NAME} PUBLIC 
    $ENV{VULKAN_SDK}/Lib/vulkan-1.lib
    glfw
    glslang
    glslang-default-resource-limits
    SPIRV
    spirv-cross-glsl
    imgui
)
set_property(TARGET glfw PROPERTY FOLDER "External")
set_property(TARGET glslang PROPERTY FOLDER "External")
set_property(TARGET glslang-default-resource-limits PROPERTY FOLDER "External")
set_property(TARGET SPIRV PROPERTY FOLDER "External")
set_property(TARGET spirv-cross PROPERTY FOLDER "External")
set_property(TARGET spirv-cross-c PROPERTY FOLDER "External")
set_property(TARGET spirv-cross-core PROPERTY FOLDER "External")
set_property(TARGET spirv-cross-glsl PROPERTY FOLDER "External")
set_property(TARGET spirv-cross-cpp PROPERTY FOLDER "External")
set_property(TARGET spirv-cross-hlsl PROPERTY FOLDER "External")
set_property(TARGET spirv-cross-msl PROPERTY FOLDER "External")
set_property(TARGET spirv-cross-reflect PROPERTY FOLDER "External")
set_property(TARGET spirv-cross-util PROPERTY FOLDER "External")
set_property(TARGET imgui PROPERTY FOLDER "External")

target_include_directories(
    ${PROJECT_NAME} PUBLIC
    "${PROJECT_SOURCE_DIR}/external/vulkan/include"
    "${PROJECT_SOURCE_DIR}/external/VulkanMemoryAllocator/include"
    "${PROJECT_SOURCE_DIR}/external/glfw/include"
    "${PROJECT_SOURCE_DIR}/external/glm"
    "${PROJECT_SOURCE_DIR}/external/tinyobjloader"
    "${PROJECT_SOURCE_DIR}/external/tinygltf"
    "${PROJECT_SOURCE_DIR}/external/glslang"
    "${PROJECT_SOURCE_DIR}/external/SPIRV-Cross"
    "${PROJECT_SOURCE_DIR}/external/spdlog/include"
    "${PROJECT_SOURCE_DIR}/external/imgui"
    "${PROJECT_SOURCE_DIR}/external/imgui/backends"
    "${PROJECT_SOURCE_DIR}/external/imgui-vulkan-hpp-backend"
)
