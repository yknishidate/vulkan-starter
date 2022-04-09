cmake_minimum_required(VERSION 3.10)
project(vk LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 20)

add_subdirectory(external/glfw)
add_subdirectory(external/glslang)
add_subdirectory(external/SPIRV-Cross)

file(GLOB sources source/*.cpp)
add_executable(${PROJECT_NAME} 
    ${sources}
    external/imgui/backends/imgui_impl_glfw.cpp
    external/imgui/backends/imgui_impl_vulkan.cpp
    external/imgui/imgui_demo.cpp
    external/imgui/imgui_draw.cpp
    external/imgui/imgui_tables.cpp
    external/imgui/imgui.cpp
    external/imgui/imgui_widgets.cpp
)

target_link_libraries(
    ${PROJECT_NAME} PUBLIC 
    $ENV{VULKAN_SDK}/Lib/vulkan-1.lib
    glfw
    glslang
    glslang-default-resource-limits
    SPIRV
    spirv-cross-glsl
)

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
)
