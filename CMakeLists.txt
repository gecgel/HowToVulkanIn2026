cmake_minimum_required(VERSION 4.0)
project(HowToVulkanIn2026)

add_executable(App
    "${CMAKE_SOURCE_DIR}/sources/main.cpp"
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
