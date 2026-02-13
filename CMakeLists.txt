cmake_minimum_required(VERSION 4.0)
project(HowToVulkanIn2026)

find_package(Vulkan REQUIRED)

include(FetchContent)

FetchContent_Declare(
    sdl
    GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
    GIT_TAG release-3.2.28
    GIT_SHALLOW ON
    GIT_PROGRESS ON
)
FetchContent_MakeAvailable(sdl)

FetchContent_Declare(
    volk
    GIT_REPOSITORY https://github.com/zeux/volk
    GIT_TAG vulkan-sdk-1.4.341.0
    GIT_SHALLOW ON
    GIT_PROGRESS ON
)
FetchContent_MakeAvailable(volk)

FetchContent_Declare(
    vma
    GIT_REPOSITORY https://github.com/GPUOpen-LibrariesAndSDKs/VulkanMemoryAllocator
    GIT_TAG v3.3.0
    GIT_SHALLOW ON
    GIT_PROGRESS ON
)
FetchContent_MakeAvailable(vma)

FetchContent_Declare(
    glm
    GIT_REPOSITORY https://github.com/g-truc/glm
    GIT_TAG 1.0.3
    GIT_SHALLOW ON
    GIT_PROGRESS ON
)
FetchContent_MakeAvailable(glm)

FetchContent_Declare(
    slang
    GIT_REPOSITORY https://github.com/shader-slang/slang
    GIT_TAG v2026.2.1
    GIT_SHALLOW ON
    GIT_PROGRESS ON
)
FetchContent_MakeAvailable(slang)

FetchContent_Declare(
    ktx_software
    GIT_REPOSITORY https://github.com/KhronosGroup/KTX-Software
    GIT_TAG v4.4.2
    GIT_SHALLOW ON
    GIT_PROGRESS ON
)
FetchContent_MakeAvailable(ktx_software)

FetchContent_Declare(
    tinyobjloader
    GIT_REPOSITORY https://github.com/tinyobjloader/tinyobjloader
    GIT_TAG release
    GIT_SHALLOW ON
    GIT_PROGRESS ON
)
FetchContent_MakeAvailable(tinyobjloader)

add_executable(App
    "${CMAKE_SOURCE_DIR}/sources/main.cpp"
)

target_link_libraries(App PRIVATE
    Vulkan::Vulkan
    SDL3::SDL3
    volk::volk
    GPUOpen::VulkanMemoryAllocator
    glm::glm
    slang
    ktx
    tinyobjloader
)

set_target_properties(App PROPERTIES
    CXX_EXCEPTIONS OFF
    CXX_EXTENSIONS OFF
    CXX_SCAN_FOR_MODULES OFF
    CXX_STANDARD 23
    CXX_STANDARD_REQUIRED ON
)

if(CMAKE_CXX_COMPILER_ID STREQUAL "Clang" AND CMAKE_CXX_COMPILER_FRONTEND_VARIANT STREQUAL "GNU")
    # cSpell: disable
    target_compile_options(App PRIVATE
        "-Weverything"
        "-Wno-c++98-compat"
        "-Wno-unsafe-buffer-usage-in-libc-call"
    )
    # cSpell: enable
endif()
