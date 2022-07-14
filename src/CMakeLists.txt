set(SOURCE_FILES
    main.cpp
)

set(HEADER_FILES
)

if (WIN32)

set(CURSES_LIBS
    ${CMAKE_SOURCE_DIR}/PDCurses/pdcurses.lib
)

else()

set(CURSES_LIBS
    ${CMAKE_SOURCE_DIR}/ncurses/lib/libform.a
    ${CMAKE_SOURCE_DIR}/ncurses/lib/libmenu.a
    ${CMAKE_SOURCE_DIR}/ncurses/lib/libncurses++.a
    ${CMAKE_SOURCE_DIR}/ncurses/lib/libncurses.a
    ${CMAKE_SOURCE_DIR}/ncurses/lib/libpanel.a
)

endif()

add_executable(main
    ${SOURCE_FILES}
    ${HEADER_FILES}
    ${RESOURCE_FILES}
)

target_link_libraries(main
    PUBLIC
        ${CONAN_LIBS}
        ${CURSES_LIBS}

)

target_include_directories(main
PUBLIC 
    ${CONAN_INCLUDE_DIRS}
)


