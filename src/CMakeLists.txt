
set(RE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(RE_SRCS "")
set(RE_LIBS "")
set(RE_INCLUDES "")
set(RE_DEFINITIONS "")

macro (re_module_add)
    file (RELATIVE_PATH _relPath "${RE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}")
    foreach (_src ${ARGN})
        if (_relPath)
            list (APPEND RE_SRCS "${_relPath}/${_src}")
        else()
            list (APPEND RE_SRCS "${_src}")
        endif()
    endforeach()
    if (_relPath)
        set (RE_SRCS ${RE_SRCS} PARENT_SCOPE)
    endif()
endmacro()

macro (re_include_directory_add)
    file (RELATIVE_PATH _relPath "${RE_DIR}" "${CMAKE_CURRENT_SOURCE_DIR}")
    foreach (_inc ${ARGN})
                if (IS_ABSOLUTE ${_inc})
                            list (APPEND RE_INCLUDES "${_inc}")
                else()
                    if (_relPath)
                            list (APPEND RE_INCLUDES "${_relPath}/${_inc}")
                    else()
                            list (APPEND RE_INCLUDES "${_inc}")
                    endif()
                endif()
    endforeach()
    if (_relPath)
        set (RE_INCLUDES ${RE_INCLUDES} PARENT_SCOPE)
    endif()
endmacro()

macro (re_library_add)
    foreach (_lib ${ARGN})
            list (APPEND RE_LIBS "${_lib}")
    endforeach()
     set (RE_LIBS ${RE_LIBS} PARENT_SCOPE)
endmacro()

macro (re_definition_add)
    foreach (_define ${ARGN})
            list (APPEND RE_DEFINITIONS "${_define}")
    endforeach()
     set (RE_DEFINITIONS ${RE_DEFINITIONS} PARENT_SCOPE)
endmacro()

set(RE_MODULES
    sip sipevent sipreg sipsess
    uri http httpauth msg websock
    stun turn ice
    natbd
    rtp sdp jbuf telev
    dns
    md5 crc32 sha hmac base64
    udp sa net tcp tls
    list mbuf hash
    fmt tmr main mem dbg sys lock mqueue
    mod conf
    bfcp
    aes srtp
    odict
    json)

foreach(DIR ${RE_MODULES})
	add_subdirectory(${DIR})
endforeach()

list(REMOVE_DUPLICATES RE_DEFINITIONS)
list(REMOVE_DUPLICATES RE_LIBS)
list(REMOVE_DUPLICATES RE_INCLUDES)
include_directories(${RE_INCLUDES})

add_library(re ${RE_SRCS})
set_target_properties(${MODULE_NAME} PROPERTIES LINKER_LANGUAGE C)

add_definitions(${RE_DEFINITIONS})
target_link_libraries(re ${RE_LIBS})
