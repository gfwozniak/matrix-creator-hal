project(matrix_creator_hal C CXX)
cmake_minimum_required(VERSION 3.2)

set(CMAKE_BUILD_TYPE Release)

find_library (FFTW_LIBRARIES NAMES fftw3f )
FIND_LIBRARY(LGPIO_LIB NAMES lgpio)

message(${LGPIO_LIB})

add_compile_options(-std=c++11)

# Enable extra warnings. Not needed.
include (../../cmake/FatalWarnings.cmake)
ADM_EXTRA_WARNINGS()

find_package(Threads)

include_directories(
  ../..
)

set(matrix_creator_hal_src
  dummy_sensor.cpp
  everloop.cpp
  matrix_driver.cpp
  mcu_firmware.cpp
  microphone_array.cpp
  microphone_core.cpp
  matrixio_bus.cpp
  cross_correlation.cpp
  direction_of_arrival.cpp
  audio_output.cpp
  bus_direct.cpp
  bus_kernel.cpp
)

add_library(matrix_creator_hal SHARED ${matrix_creator_hal_src})
  set_property(TARGET matrix_creator_hal PROPERTY CXX_STANDARD 11)
  target_link_libraries(matrix_creator_hal ${CMAKE_THREAD_LIBS_INIT} ${CMAKE_THREAD_LIBS_INIT})
  target_link_libraries(matrix_creator_hal ${FFTW_LIBRARIES})
  target_link_libraries(matrix_creator_hal ${LGPIO_LIB})

set (matrix_creator_hal_headers
  circular_queue.h
  creator_memory_map.h  
  dummy_data.h          
  dummy_sensor.h        
  everloop.h        
  everloop_image.h  
  fw_data.h          
  matrix_driver.h     
  mcu_firmware.h
  microphone_array.h 
  microphone_core.h
  microphone_core_fir.h 
  microphone_array_location.h
  matrixio_bus.h
  bus.h
  bus_direct.h
  bus_kernel.h
  cross_correlation.h
  direction_of_arrival.h
  audio_output.h
)

install (TARGETS matrix_creator_hal DESTINATION lib)

install (FILES ${matrix_creator_hal_headers} DESTINATION include/matrix_hal)
