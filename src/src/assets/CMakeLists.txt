cmake_minimum_required (VERSION 3.8)

set(RESOURCE_LIST
    ftc-main-window.ui
)

compile_gresources(RESOURCE_LIST
XML_OUT
TYPE EMBED_C
PREFIX /com/hunesion/ftcapp/
COMPRESS_ALL
RESOURCES ${RESOURCE_LIST})

add_custom_target(resource ALL DEPENDS ${RESOURCE_LIST})

get_filename_component(PARENT_DIR ${CMAKE_CURRENT_SOURCE_DIR} DIRECTORY)
message(${PARENT_DIR})
add_custom_command(TARGET resource 
                POST_BUILD
                COMMAND ${CMAKE_COMMAND} -E copy 
                ${CMAKE_CURRENT_BINARY_DIR}/resources.c
                ${PARENT_DIR}/resources.cpp
                )


