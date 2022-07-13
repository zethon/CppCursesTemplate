set(SOURCE_FILES
    main.cpp
)

set(HEADER_FILES
)

add_executable(arctan
    ${SOURCE_FILES}
    ${HEADER_FILES}
    ${RESOURCE_FILES}
)

target_link_libraries(arctan
    PUBLIC
        ${CONAN_LIBS}
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libform.a
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libmenu.a
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libncurses++.a
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libncurses.a
        ${CMAKE_SOURCE_DIR}/ncurses/lib/libpanel.a
)

target_include_directories(arctan
PUBLIC 
    ${CONAN_INCLUDE_DIRS}
)


