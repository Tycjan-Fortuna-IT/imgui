cmake_minimum_required(VERSION 3.15)

project(ImGui VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Define target
add_library(ImGui STATIC)

# Set output directories
set(OUTPUT_DIR "${CMAKE_BINARY_DIR}/bin")
set_target_properties(ImGui PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${OUTPUT_DIR}"
    LIBRARY_OUTPUT_DIRECTORY "${OUTPUT_DIR}"
    RUNTIME_OUTPUT_DIRECTORY "${OUTPUT_DIR}"
)

# Source files
set(IMGUI_SOURCES
    "imconfig.h"
    "imgui.h"
    "imgui.cpp"
    "imgui_draw.cpp"
    "imgui_internal.h"
    "imgui_widgets.cpp"
    "imstb_rectpack.h"
    "imstb_textedit.h"
    "imstb_truetype.h"
    "imgui_demo.cpp"
    "imgui_tables.cpp"
)

# Add sources to target
target_sources(ImGui PRIVATE ${IMGUI_SOURCES})

# Platform-specific settings
if(WIN32)
    target_compile_definitions(ImGui PRIVATE WINDOWS)
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Release>:Release>")
endif()

# Configuration-specific settings
if(CMAKE_BUILD_TYPE STREQUAL "Release")
    target_compile_options(ImGui PRIVATE /MT)
endif()
