# ########## Project setup ##########
PROJECT(main)
CMAKE_MINIMUM_REQUIRED(VERSION 2.4.5)

# ######### General setup ##########
INCLUDE_DIRECTORIES(${main_SOURCE_DIR})
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR})

## Automatic way ?
INCLUDE_DIRECTORIES(${PHP_SOURCE_DIR}/Zend)
INCLUDE_DIRECTORIES(${PHP_SOURCE_DIR}/TSRM)
INCLUDE_DIRECTORIES(${PHP_SOURCE_DIR}/ext/date/lib)

SET(PHP_main_LIBRARIES)
FIND_PACKAGE(ICU)
if (ICU_FOUND AND ICU_I18N_FOUND)
#  add_definitions(-DPHP_HAS_ICU=2)
        MESSAGE("Found ICU: ${ICU_INCLUDE_DIRS}")
        include_directories(${ICU_INCLUDE_DIRS})
        set(PHP_main_LIBRARIES ${ICU_LIBRARIES} ${ICU_I18N_LIBRARIES})
endif (ICU_FOUND AND ICU_I18N_FOUND)


# ########## main library ##########
# Sources:
SET(main_library_SRCS
    alloca.c
    fopen_wrappers.c
    getopt.c
    internal_functions.c
    internal_functions_cli.c
#    internal_functions_nw.c
#    internal_functions_win32.c
    main.c
    mergesort.c
    network.c
    output.c
    php_content_types.c
    php_ini.c
    php_logos.c
    php_open_temporary_file.c
    php_scandir.c
    php_sprintf.c
    php_ticks.c
    php_variables.c
    reentrancy.c
    rfc1867.c
    SAPI.c
    snprintf.c
    spprintf.c
    strlcat.c
    strlcpy.c
)

# Headers:
SET(main_library_HDRS
    build-defs.h
    config.w32.h
    fopen_wrappers.h
    logos.h
    php.h
    php_compat.h
    php_config.h
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
)

CONFIGURE_FILE(build-defs.h.in ${CMAKE_SOURCE_DIR}/build-defs.h)
CONFIGURE_FILE(internal_functions.c.in ${CMAKE_SOURCE_DIR}/internal_functions.c)
#CONFIGURE_FILE(php_config.h.in ${CMAKE_SOURCE_DIR}/php_config.h)


# actual target:
ADD_LIBRARY(main ${main_library_SRCS} ${main_library_HDRS})
SET_TARGET_PROPERTIES(main PROPERTIES VERSION 0.0.0)

# add install target:
INSTALL(TARGETS main DESTINATION lib)