SET(CMAKE_C_COMPILER "/opt/pgi/linux86-64/18.4/bin/pgcc")
SET(CMAKE_CXX_COMPILER "/opt/pgi/linux86-64/18.4/bin/pgc++")
cmake_minimum_required(VERSION 3.9)
project(mpi_acc)
#enable_language(Fortran)

find_package(MPI REQUIRED)
include_directories(${MPI_INCLUDE_PATH})

add_executable(
laplace2d.exe
laplace2d_solution.c
)

target_compile_options(laplace2d.exe PRIVATE ${MPI_CXX_COMPILE_FLAGS} -fast -acc -ta=nvidia)
target_link_libraries(laplace2d.exe ${MPI_LIBRARIES} -fast -acc -ta=nvidia)
