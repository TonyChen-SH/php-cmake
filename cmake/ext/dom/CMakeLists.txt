## CMake date File
##
## PHP License
##
## Author: Alejandro Leiva <gloob@php.net>
##
## $Id$

# Extension: dom

option(dom "Enable dom support" ON)
option(dom-shared "Shared dom" OFF)


set(EXT_DOM_SOURCES
  php_dom.c attr.c document.c domerrorhandler.c 
                            domstringlist.c domexception.c namelist.c 
                            processinginstruction.c cdatasection.c 
                            documentfragment.c domimplementation.c 
                            element.c node.c string_extend.c characterdata.c 
                            documenttype.c domimplementationlist.c entity.c 
                            nodelist.c text.c comment.c domconfiguration.c 
                            domimplementationsource.c entityreference.c 
                            notation.c xpath.c dom_iterators.c 
                            typeinfo.c domerror.c domlocator.c namednodemap.c userdatahandler.c
)

#add_library(EXT_XML [STATIC | SHARED | MODULE] [EXCLUDE_FROM_ALL]
add_library(EXT_DOM ${EXT_DOM_SOURCES})
##target_link_libraries(EXT_DOM ${@@EXTENSION_LIBRARIES@@})
