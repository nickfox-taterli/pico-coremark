cmake_minimum_required(VERSION 3.12)

# Pull in PICO SDK (must be before project)
include(pico_sdk_import.cmake)

project(pico_examples C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "-O3 -Wall -Wextra")

set(PICO_EXAMPLES_PATH ${PROJECT_SOURCE_DIR})

# Initialize the SDK
pico_sdk_init()

include_directories("coremark")
aux_source_directory(./coremark src_coremark)
add_executable(coremark ${src_coremark} )

# Pull in our pico_stdlib which aggregates commonly used features
target_link_libraries(coremark pico_stdlib)
pico_set_binary_type(coremark no_flash)

# create map/bin/hex/uf2 file etc.
pico_add_extra_outputs(coremark)
