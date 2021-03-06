project(ISO5436_2)

cmake_minimum_required(VERSION 2.8)

INCLUDE (FindPkgConfig)

find_package(ZLIB) 

if ( ZLIB_FOUND )
    include_directories( ${ZLIB_INCLUDE_DIRS} )
else ( ZLIB_FOUND )
    add_subdirectory(zlib) 
    include_directories(${CMAKE_CURRENT_SOURCE_DIR}/zlib)
    include_directories(${CMAKE_CURRENT_BINARY_DIR}/zlib)
    set(ZLIB_LIBRARIES "zlib")
endif( ZLIB_FOUND )

if (PKG_CONFIG_FOUND)
    PKG_CHECK_MODULES(MINIZIP minizip)
else (PKG_CONFIG_FOUND)
    set (MINIZIP_FOUND FALSE)
endif(PKG_CONFIG_FOUND)

if ( MINIZIP_FOUND )
    include_directories( ${MINIZIP_INCLUDE_DIRS} )
else ( MINIZIP_FOUND )
    add_subdirectory(zlib/contrib/minizip) 
    set(MINIZIP_LIBRARIES "zlibwapi")
	if (WIN32)
	    set(ZLIB_LIBRARIES "")
	endif(WIN32)
endif ( MINIZIP_FOUND )
 
add_subdirectory(ISO5436_2_XML) 
