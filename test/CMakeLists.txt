find_package(SDL2main)
find_package(SDL2test REQUIRED)

add_executable(testfont main.c)

set(ALL_TESTS
    testfont
)

foreach(prog ${ALL_TESTS})
    if(TARGET SDL2::SDL2main)
        target_link_libraries(${prog} PRIVATE SDL2::SDL2main)
    endif()
    target_link_libraries(${prog} PRIVATE SDL2::SDL2test ${sdl2_target_name} SDL2_ttf)

    add_test(
        NAME ${prog}
        COMMAND ${prog}
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    )
    set_tests_properties(
        ${prog}
        PROPERTIES
        ENVIRONMENT "${TESTS_ENVIRONMENT}"
        TIMEOUT 30
    )
endforeach()
