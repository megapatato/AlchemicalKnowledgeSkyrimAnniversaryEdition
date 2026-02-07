# This file configures the "build" of this SKSE plugin
# - how to compile the C++ plugin (in addition to settings found in CMakePresets.json)
# - where to output the resulting .dll file

# It's recommended to set a minimum CMake version.
# If you use CMake features from higher versions, update this to match.
cmake_minimum_required(VERSION 3.21)
project(AlchemicalKnowledge VERSION 0.0.1 LANGUAGES CXX)

# Setup as an SKSE plugin
find_package(CommonLibSSE CONFIG REQUIRED)
add_commonlibsse_plugin(${PROJECT_NAME} SOURCES plugin.cpp) # <--- specifies plugin.cpp
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_23) # <--- use C++23 standard
target_precompile_headers(${PROJECT_NAME} PRIVATE PCH.h) # <--- PCH.h is required!

# Setup installation rules
set(OUTPUT_FOLDER "$ENV{APPDATA}/Vortex/skyrimse/mods/${PROJECT_NAME}")

install(
    TARGETS "${PROJECT_NAME}"
    RUNTIME
    DESTINATION "${OUTPUT_FOLDER}/SKSE/Plugins"
)

install(
    FILES "creation engine/compiled esp/AlchemicalKnowledge.esp"
    DESTINATION "${OUTPUT_FOLDER}"
)
