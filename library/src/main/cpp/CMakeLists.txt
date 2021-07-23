# FFmpegAudioPlayer
# 2021/07/24 Moriafly

# CMake 最低版本要求
cmake_minimum_required(VERSION 3.10.2)

# 支持 gnu++11
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")

# 定义 ffmpeg so 库和头文件所在目录，方便后续使用
set(ffmpeg_lib_dir ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI})
set(ffmpeg_head_dir ${CMAKE_SOURCE_DIR}/ffmpeg)

# 添加 ffmpeg 头文件目录
include_directories(${ffmpeg_head_dir}/include)

# 添加ffmpeg相关的so库
add_library(avutil
        SHARED
        IMPORTED)
set_target_properties(avutil
        PROPERTIES IMPORTED_LOCATION
        ${ffmpeg_lib_dir}/libavutil.so)

add_library(swresample
        SHARED
        IMPORTED)
set_target_properties(swresample
        PROPERTIES IMPORTED_LOCATION
        ${ffmpeg_lib_dir}/libswresample.so)

add_library(avcodec
        SHARED
        IMPORTED)
set_target_properties(avcodec
        PROPERTIES IMPORTED_LOCATION
        ${ffmpeg_lib_dir}/libavcodec.so)

add_library(avfilter
        SHARED
        IMPORTED)
set_target_properties(avfilter
        PROPERTIES IMPORTED_LOCATION
        ${ffmpeg_lib_dir}/libavfilter.so)

add_library(swscale
        SHARED
        IMPORTED)
set_target_properties(swscale
        PROPERTIES IMPORTED_LOCATION
        ${ffmpeg_lib_dir}/libswscale.so)

add_library(avformat
        SHARED
        IMPORTED)
set_target_properties(avformat
        PROPERTIES IMPORTED_LOCATION
        ${ffmpeg_lib_dir}/libavformat.so)

add_library(postproc
        SHARED
        IMPORTED)
set_target_properties(postproc
        PROPERTIES IMPORTED_LOCATION
        ${ffmpeg_lib_dir}/libpostproc.so)

# 查找代码中使用到的系统库
find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log )

file(GLOB ffmpeg_audio_player_srcs_cpp "*.cpp")
file(GLOB ffmpeg_audio_player_srcs_c "*.c")

add_library( # Sets the name of the library.
        ffmpeg-audio-player

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        ${ffmpeg_audio_player_srcs_cpp}
        ${ffmpeg_audio_player_srcs_c}
        )

# 指定编译目标库时，cmake要链接的库
target_link_libraries(
        # 指定目标库
        ffmpeg-audio-player

        # 连接 FFmpeg 相关的库
        avformat
        avcodec
        avfilter
        avutil
        swresample
        swscale
        postproc

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib}
)
