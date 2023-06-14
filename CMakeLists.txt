cmake_minimum_required(VERSION 3.25)
project(minimal_fortran_scikit_build_core_cibuildwheel_example LANGUAGES Fortran)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

set(BUILD_TESTING OFF)
include(FetchContent)
FetchContent_Declare(
        fortran_stdlib
        GIT_REPOSITORY https://github.com/fortran-lang/stdlib.git
        GIT_TAG fb4ca801f0c8e0ed09f9d137c620676fa348ebdd  # v0.2.1
)
FetchContent_MakeAvailable(fortran_stdlib)
set(BUILD_TESTING ON)

add_library(minimal_fortran_scikit_build_core_cibuildwheel_example SHARED main.f90)
target_link_libraries(minimal_fortran_scikit_build_core_cibuildwheel_example PUBLIC fortran_stdlib)

set(library_directory "${SKBUILD_PLATLIB_DIR}/lib")
install(TARGETS minimal_fortran_scikit_build_core_cibuildwheel_example DESTINATION library_directory)