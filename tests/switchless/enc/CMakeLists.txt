# Copyright (c) Open Enclave SDK contributors.
# Licensed under the MIT License.

set (EDL_FILE ../switchless.edl)

add_custom_command(
    OUTPUT switchless_t.h switchless_t.c
    DEPENDS ${EDL_FILE} edger8r
    COMMAND edger8r --trusted ${EDL_FILE} --search-path ${CMAKE_CURRENT_SOURCE_DIR})

add_enclave(TARGET switchless_enc UUID d497e154-9e8e-4029-a53d-c0a36533fb95 SOURCES enc.c ${CMAKE_CURRENT_BINARY_DIR}/switchless_t.c)

target_include_directories(switchless_enc PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(switchless_enc oelibc)
