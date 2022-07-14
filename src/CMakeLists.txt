set(SOURCE_FILES
    main.cpp
)

set(HEADER_FILES
)

add_executable(main
    ${SOURCE_FILES}
    ${HEADER_FILES}
    ${RESOURCE_FILES}
)

target_link_libraries(main
    PUBLIC
        ${CONAN_LIBS}
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libform.a
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libmenu.a
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libncurses++.a
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libncurses.a
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libpanel.a
)

target_include_directories(main
PUBLIC 
    ${CONAN_INCLUDE_DIRS}
)


