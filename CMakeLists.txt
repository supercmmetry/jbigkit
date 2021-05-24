cmake_minimum_required(VERSION 3.17)
project(jbigkit)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

include_directories(libjbig)

add_executable(tstcodec
        libjbig/jbig.h
        libjbig/tstcodec.c)

add_executable(tstcodec85
        libjbig/jbig85.h
        libjbig/tstcodec85.c)

add_library(jbig_ar STATIC
        libjbig/jbig_ar.h
        libjbig/jbig_ar.c)

add_library(jbig STATIC
        libjbig/jbig.h
        libjbig/jbig.c
        libjbig/jbig_ar.h
        libjbig/jbig_ar.c)

add_library(jbig85 STATIC
        libjbig/jbig85.h
        libjbig/jbig85.c
        libjbig/jbig_ar.h
        libjbig/jbig_ar.c)

target_link_libraries(tstcodec PUBLIC jbig)
target_link_libraries(tstcodec85 PUBLIC jbig85)

install(TARGETS tstcodec tstcodec85 DESTINATION bin)
install(TARGETS jbig jbig85 jbig_ar DESTINATION lib)
