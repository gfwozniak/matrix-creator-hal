cmake_minimum_required(VERSION 3.2)
project(MatrixHAL)

# Add -Wall and -Wextra. Also,
# treat C/C++ warnings as errors if -DADM_FATAL_WARNINGS=ON.
include (cmake/FatalWarnings.cmake)
ADM_EXTRA_WARNINGS()

add_subdirectory(demos)


