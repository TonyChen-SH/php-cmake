## CMake date File
##
## PHP License
##
## Author: Alejandro Leiva <gloob@php.net>
##
## $Id$

# Extension: iconv

option(iconv "Enable iconv support" ON)
option(iconv-shared "Shared iconv" OFF)

file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/php_have_bsd_iconv.h)
file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/php_have_glibc_iconv.h)
file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/php_have_libiconv.h)
file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/php_have_ibm_iconv.h)

file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/php_have_iconv.h)
file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/php_iconv_supports_errno.h)
file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/php_php_iconv_impl.h)
file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/php_php_iconv_h_path.h)

set(HAVE_ICONV 1)

find_package(ICONV)
if(ICONV_FOUND)
  message("ICONV Found")
endif(ICONV_FOUND)

set(EXT_ICONV_SOURCES
  iconv.c
)

#add_library(EXT_XML [STATIC | SHARED | MODULE] [EXCLUDE_FROM_ALL]
add_library(EXT_ICONV ${EXT_ICONV_SOURCES})
if(ICONV_FOUND)
  target_link_libraries(EXT_ICONV ${ICONV_LIBRARY})
endif(ICONV_FOUND)

