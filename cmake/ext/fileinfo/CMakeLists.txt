## CMake date File
##
## PHP License
##
## Author: Alejandro Leiva <gloob@php.net>
##
## $Id$

# Extension: fileinfo

option(fileinfo "Enable fileinfo support" ON)
option(fileinfo-shared "Shared fileinfo" OFF)

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/libmagic")

file(GLOB_RECURSE EXT_FILEINFO_SOURCES "*.h" "*.c" "libmagic/*.c" "libmagic/*.h")
#add_library(EXT_XML [STATIC | SHARED | MODULE] [EXCLUDE_FROM_ALL]
add_library(EXT_FILEINFO ${EXT_FILEINFO_SOURCES})
##target_link_libraries(EXT_FILEINFO ${@@EXTENSION_LIBRARIES@@})
