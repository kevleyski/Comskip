cmake_minimum_required(VERSION 3.14)
project(Comskip)

set(CMAKE_CXX_STANDARD 14)

include_directories(.)
include_directories(ccextratorwin)
include_directories(vendor)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "-D__STDC_CONSTANT_MACROS -DPROCESS_CC")
set(CMAKE_C_FLAGS "-D__STDC_CONSTANT_MACROS -DPROCESS_CC")

find_path(AVCODEC_INCLUDE_DIR libavcodec/avcodec.h)
find_library(AVCODEC_LIBRARY avcodec)

find_path(AVFORMAT_INCLUDE_DIR libavformat/avformat.h)
find_library(AVFORMAT_LIBRARY avformat)

find_path(AVUTIL_INCLUDE_DIR libavutil/avutil.h)
find_library(AVUTIL_LIBRARY avutil)

find_path(AVDEVICE_INCLUDE_DIR libavdevice/avdevice.h)
find_library(AVDEVICE_LIBRARY avdevice)

find_path(SDL_INCLUDE_DIR sdl.h)
find_library(SDL_LIBRARY sdl)

add_executable(Comskip
        ccextratorwin/608.c
        ccextratorwin/608.h
        ccextratorwin/ccextractor.c
        ccextratorwin/ccextractor.h
        ccextratorwin/encoding.c
        ccextratorwin/general_loop.c
        ccextratorwin/myth.c
        vendor/argtable2.h
        comskip.c
        comskip.h
        config.h
        DDRAW.H
        mpeg2dec.c
        platform.c
        platform.h
        resource.h
        video_out_dx.c
        video_out_sdl.c
        vo.h
        win32_pthread.c
        win32_pthread.h)

target_include_directories(Comskip PRIVATE ${AVCODEC_INCLUDE_DIR} ${AVFORMAT_INCLUDE_DIR} ${AVUTIL_INCLUDE_DIR} ${AVDEVICE_INCLUDE_DIR})
target_link_libraries(Comskip PRIVATE ${AVCODEC_LIBRARY} ${AVFORMAT_LIBRARY} ${AVUTIL_LIBRARY} ${AVDEVICE_LIBRARY})
