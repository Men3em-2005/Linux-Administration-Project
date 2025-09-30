add_executable(output
    app.c
)

target_link_libraries(output
    caesar
    xor
)

set_target_properties(output PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

add_custom_command(TARGET output POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E make_directory ${CMAKE_CURRENT_SOURCE_DIR}/out/libs
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:xor> ${CMAKE_CURRENT_SOURCE_DIR}/out/libs/
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:caesar> ${CMAKE_CURRENT_SOURCE_DIR}/out/libs/
)

set_target_properties(output PROPERTIES
    BUILD_RPATH "\$ORIGIN/out/libs"
)