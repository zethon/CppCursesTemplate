cmake_minimum_required(VERSION 3.0)

project(ttvg)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_MACOSX_RPATH 1)

# optional configuration
option(BUILD_UNIT_TESTS "Build unit tests (default OFF)" OFF)
option(SHARED_SFML "Use shared SFML libraries (default OFF)" ON)

# initialize conan libs
include(CMake/conan.cmake)
conan_cmake_run(REQUIRES
    boost/1.77.0
    spdlog/1.9.2
    BASIC_SETUP CMAKE_TARGETS
    GENERATORS cmake_find_package cmake_paths
    BUILD missing
    OPTIONS 
        boost:shared=False 
        boost:without_test=False 
        boost:without_program_options=False 
        boost:without_filesystem=False 
        boost:without_system=False 
        boost:without_exception=False
        boost:without_contract=False
)
include(${CMAKE_BINARY_DIR}/conan_paths.cmake)
include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(NO_OUTPUT_DIRS KEEP_RPATHS)

# Add a RELEASE definition that we can count on regardless
# of platform
string(APPEND CMAKE_CXX_FLAGS_RELEASE " -DRELEASE")
string(APPEND CMAKE_CXX_FLAGS_MINSIZEREL " -DRELEASE")

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})

find_package(Boost COMPONENTS)
include_directories(${Boost_INCLUDE_DIRS})

if (MSVC)
    add_definitions(
        -DWIN32
        -D_WIN32
        -D_WINDOWS
        -D_WIN32_WINDOWS
        -DNOMINMAX
        -D_SCL_SECURE_NO_WARNINGS
        -DWIN32_LEAN_AND_MEAN

        # use this to supress the boost generated "warning C4996"
        # on Windows
        -D_SILENCE_FPOS_SEEKPOS_DEPRECATION_WARNING
    )

    add_compile_options(
        # treat warnings as errors
        /WX
        /wd4996
    )

    add_link_options(
        # eliminate a lot of debug linking errors
        /IGNORE:4099
    )
endif(MSVC)

include(ExternalProject)
ExternalProject_Add(
  libncurses
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/ncurses
  CONFIGURE_COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/ncurses/configure
  PREFIX ${CMAKE_CURRENT_SOURCE_DIR}/ncurses
  BUILD_COMMAND make
  BUILD_IN_SOURCE 1
)

add_subdirectory(arctan)
