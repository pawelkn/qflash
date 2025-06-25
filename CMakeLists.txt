cmake_minimum_required(VERSION 3.10)
project(QFlash C CXX)

set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 11)

# Source files
set(FASTBOOT_FILES
    fastboot/protocol.c
    fastboot/engine.c
    fastboot/fastboot.c
    fastboot/usb_linux_fastboot.c
    fastboot/util_linux.c
)

set(FIREHOSE_FILES
    firehose/qfirehose.c
    firehose/sahara_protocol.c
    firehose/firehose_protocol.c
    firehose/usb_linux.c
)

set(QFLASH_FILES
    tinystr.cpp
    tinyxml.cpp
    tinyxmlerror.cpp
    tinyxmlparser.cpp
    md5.cpp
    at_tok.cpp
    atchannel.cpp
    ril-daemon.cpp
    download.cpp
    file.cpp
    os_linux.cpp
    serialif.cpp
    quectel_log.cpp
    quectel_common.cpp
    quectel_crc.cpp
    check_env.cpp
)

# Object files for C sources
add_library(fastboot_objs OBJECT ${FASTBOOT_FILES})
add_library(firehose_objs OBJECT ${FIREHOSE_FILES})

# Add definitions
add_definitions(-DPROGRESS_FILE_FAETURE)
add_definitions(-DUSE_FASTBOOT)
add_definitions(-DFIREHOSE_ENABLE)

# Main executable
add_executable(QFlash
    $<TARGET_OBJECTS:fastboot_objs>
    $<TARGET_OBJECTS:firehose_objs>
    ${QFLASH_FILES}
)

target_link_libraries(QFlash rt pthread)

# Debug build type
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -DDEBUG")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DDEBUG")

# Install target
install(TARGETS QFlash DESTINATION bin)
