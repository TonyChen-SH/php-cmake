# PHP main zone.
#
# PHP License
#
# Author: Alejandro Leiva <gloob@php.net>
#
# $Id$

project(main C)

# Includes
include(php/PHP_INTERNAL_FUNCTIONS)

#message("$$ including: ${CMAKE_CURRENT_SOURCE_DIR}")
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

#include_directories(${CMAKE_SOURCE_DIR})

## Automatic way ? <- REFACTOR THIS
include_directories(${PHP_SOURCE_DIR}/Zend)
include_directories(${PHP_BINARY_DIR}/Zend)
include_directories(${PHP_SOURCE_DIR}/TSRM)
include_directories(${PHP_BINARY_DIR}/ext/date/lib)



set(PHP_main_LIBRARIES)

PHP_INTERNAL_FUNCTIONS("${EXTENSION_NAME_LIST}" "${EXTENSION_NAME_LIST}" ${main_BINARY_DIR}/internal_functions.c)
PHP_INTERNAL_FUNCTIONS("${EXTENSION_NAME_LIST}" "${EXTENSION_NAME_LIST}" ${main_BINARY_DIR}/internal_functions_cli.c)

configure_file(internal_functions.c.in ${CMAKE_CURRENT_SOURCE_DIR}/internal_functions.c)

# ########## main library ##########
# Sources:
set(main_library_SRCS
    internal_functions.c
    internal_functions_cli.c
#    internal_functions_nw.c
#    internal_functions_win32.c
    main.c
    snprintf.c
    spprintf.c
    php_sprintf.c
    fopen_wrappers.c
    alloca.c
    php_scandir.c
    php_ini.c
    SAPI.c
    rfc1867.c
    php_content_types.c
    strlcpy.c
    strlcat.c
    mergesort.c
    reentrancy.c
    php_variables.c
    php_ticks.c
    network.c
    php_open_temporary_file.c
    php_logos.c
    output.c
    getopt.c

    streams/streams.c
    streams/cast.c
    streams/memory.c
    streams/filter.c
    streams/plain_wrapper.c
    streams/userspace.c
    streams/transports.c
    streams/xp_socket.c
    streams/mmap.c
    streams/glob_wrapper.c
    streams/unicode_filter.c
)

file(GLOB_RECURSE main_library_SRCS "*.c")


# Headers:
set(main_library_HDRS
    build-defs.h
    fopen_wrappers.h
    logos.h
    php.h
    php_compat.h
#    php_config.h
    php_content_types.h
    php_getopt.h
    php_globals.h
    php_ini.h
    php_logos.h
    php_main.h
    php_memory_streams.h
    php_network.h
    php_open_temporary_file.h
    php_output.h
    php_reentrancy.h
    php_scandir.h
    php_streams.h
    php_syslog.h
    php_ticks.h
    php_variables.h
    php_version.h
    rfc1867.h
    SAPI.h
    snprintf.h
    spprintf.h
    win95nt.h

    streams/php_stream_filter_api.h
)

file(GLOB_RECURSE main_library_HDRS "*.h")

# actual target:
add_library(main ${main_library_SRCS} ${main_library_HDRS})
set_target_properties(main PROPERTIES VERSION 0.0.0)

# add install target:
install(TARGETS main DESTINATION lib)
