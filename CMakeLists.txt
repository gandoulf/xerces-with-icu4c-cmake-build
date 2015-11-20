cmake_minimum_required(VERSION 2.8)

project(internal)

set(CMAKE_C_FLAGS "-O3")
set(CMAKE_CXX_FLAGS "-O3")

if(NOT ANDROID)
message(STATUS "search for JNI")
find_package(JNI REQUIRED)
include_directories(${JNI_INCLUDE_DIRS})
endif()

set( LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/lib/pc CACHE PATH
        "Single Directory for all Libraries")

file(GLOB XERCES
    "xercesc/internal/*.cpp"
    "xercesc/internal/*.hpp"
    "xercesc/framework/*.cpp"
    "xercesc/framework/*.hpp"
    "xercesc/framework/psvi/*.cpp"
    "xercesc/framework/psvi/*.hpp"
    "xercesc/validators/schema/*.cpp"
    "xercesc/validators/schema/*.hpp"
    "xercesc/validators/schema/identity/*.cpp"
    "xercesc/validators/schema/identity/*.hpp"
    "xercesc/validators/common/*.cpp"
    "xercesc/validators/common/*.hpp"
    "xercesc/validators/DTD/*.cpp"
    "xercesc/validators/DTD/*.hpp"
    "xercesc/validators/datatype/*.cpp"
    "xercesc/validators/datatype/*.hpp"
    "xercesc/parsers/*.cpp"
    "xercesc/parsers/*.hpp"
    "xercesc/sax/*.cpp"
    "xercesc/sax/*.hpp"
    "xercesc/dom/*.cpp"
    "xercesc/dom/*.hpp"
    "xercesc/dom/impl/*.cpp"
    "xercesc/dom/impl/*.hpp"
    "xercesc/util/*.cpp"
    "xercesc/util/*.hpp"
    "xercesc/util/regx/*.cpp"
    "xercesc/util/regx/*.hpp"
    "xercesc/util/NetAccessors/*.cpp"
    "xercesc/util/NetAccessors/*.hpp"
    "xercesc/util/NetAccessors/Socket/*.cpp"
    "xercesc/util/NetAccessors/Socket/*.hpp"
    "xercesc/xinclude/*.cpp"
    "xercesc/xinclude/*.hpp"
    "xercesc/util/MsgLoaders/ICU/*.cpp"
    "xercesc/util/MsgLoaders/ICU/*.hpp"
    #"xercesc/util/MsgLoaders/MsgCatalog/*.cpp"
    #"xercesc/util/MsgLoaders/MsgCatalog/*.hpp"
    "xercesc/util/Transcoders/ICU/*.cpp"
    "xercesc/util/Transcoders/ICU/*.hpp"
    "xercesc/util/FileManagers/PosixFileMgr.cpp"
    "xercesc/util/FileManagers/PosixFileMgr.hpp"
    "xercesc/util/MutexManagers/NoThreadMutexMgr.cpp"
    "xercesc/util/MutexManagers/NoThreadMutexMgr.hpp"
    "*.c"
    "*.h"
    "xercesc_messages.c"
    "root_res.c"
)

add_definitions("-DHAVE_SYS_TIME_H"
		"-DHAVE_LIMITS_H"
		"-DHAVE_UNISTD_H"
		"-DHAVE_SYS_SOCKET_H"
		"-DHAVE_NETINET_IN_H"
		"-DHAVE_ARPA_INET_H"
		"-DHAVE_NETDB_H"
		"-DHAVE_STRING_H"
		"-DHAVE_STRINGS_H"
		"-DHAVE_STRNCASECMP"
		"-DHAVE_STRCASECMP"
		"-DXERCES_USE_MSGLOADER_ICU"
		"-DXERCES_USE_TRANSCODER_ICU"
		"-DXERCES_USE_FILEMGR_POSIX"
		"-DXERCES_USE_MUTEXMGR_NOTHREAD"
		"-DHAVE_GETTIMEOFDAY"
		)

include_directories(/home/resse/Android/android-lib/xerces-c-3.1.2/src)

set(NDK_LIB $ENV{SYSROOT}/usr/lib)
link_directories(${NDK_LIB})

add_library(xerces-c-3.1 SHARED ${XERCES})

target_link_libraries(xerces-c-3.1
                        -licuuc
                        -licudata
                        -ldl
                        -lm
                        -licui18n
                        -lstdc++
			/home/resse/android-toolchain/sysroot/usr/lib/rs/libRScpp_static.a
                        )