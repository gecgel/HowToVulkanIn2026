cmake_minimum_required(VERSION 4.0)
project(HowToVulkanIn2026)

find_package(Vulkan REQUIRED)
find_package(SDL3 CONFIG REQUIRED)
find_package(volk CONFIG REQUIRED)
find_package(VulkanMemoryAllocator CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(slang CONFIG REQUIRED)
find_package(ktx CONFIG REQUIRED)
find_package(tinyobjloader CONFIG REQUIRED)

add_executable(Tutorial
    "${CMAKE_SOURCE_DIR}/sources/tutorial.cpp"
)

target_link_libraries(Tutorial PRIVATE
    Vulkan::Vulkan
    SDL3::SDL3
    volk::volk_headers
    GPUOpen::VulkanMemoryAllocator
    glm::glm-header-only
    slang::slang
    KTX::ktx
    tinyobjloader::tinyobjloader
)

set_target_properties(Tutorial PROPERTIES
    CXX_SCAN_FOR_MODULES OFF
    CXX_STANDARD 20
    CXX_STANDARD_REQUIRED ON
)

add_executable(App
    "${CMAKE_SOURCE_DIR}/sources/main.cpp"
)

target_link_libraries(App PRIVATE
    Vulkan::Vulkan
    SDL3::SDL3
    volk::volk_headers
    GPUOpen::VulkanMemoryAllocator
    glm::glm-header-only
    slang::slang
    KTX::ktx
    tinyobjloader::tinyobjloader
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
