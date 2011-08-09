

project(tiff)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
include(dist.cmake)

MACRO(ADD_PREFIX prefix rootlist)
  SET(outlist )
  FOREACH(root ${${rootlist}})
	LIST(APPEND outlist ${prefix}${root})
  ENDFOREACH(root)
  SET(${rootlist} ${outlist})
ENDMACRO(ADD_PREFIX)


# generating config.h file:
MESSAGE("Configure: libtiff - generating tif_config.h:")
	INCLUDE (CheckIncludeFiles)
	INCLUDE (CheckFunctionExists)
	INCLUDE (CheckSymbolExists)
	INCLUDE (CheckLibraryExists)
	INCLUDE (CheckTypeSize)

	SET(CCITT_SUPPORT 1)
	SET(CHECK_JPEG_YCBCR_SUBSAMPLING 1)
	SET(CXX_SUPPORT 1)
	SET(DEFAULT_EXTRASAMPLE_AS_ALPHA 1)

	IF(MACOS)
		# TODO:
		#SET(HAVE_APPLE_OPENGL_FRAMEWORK 1)
	ENDIF()

	CHECK_INCLUDE_FILES (assert.h HAVE_ASSERT_H)
	CHECK_INCLUDE_FILES (dlfcn.h HAVE_DLFCN_H )
	CHECK_INCLUDE_FILES (fcntl.h HAVE_FCNTL_H )
	CHECK_FUNCTION_EXISTS(floor HAVE_FLOOR)
	CHECK_FUNCTION_EXISTS(getopt HAVE_GETOPT)

	SET(HAVE_IEEEFP 1) # TODO!!!

	#Define to 1 if the system has the type `int16'.
	#undef HAVE_INT16

	#Define to 1 if the system has the type `int32'.
	#undef HAVE_INT32

	#Define to 1 if the system has the type `int8'.
	#undef HAVE_INT8

	CHECK_INCLUDE_FILES (inttypes.h HAVE_INTTYPES_H )
	CHECK_FUNCTION_EXISTS(isascii HAVE_ISASCII)
	CHECK_FUNCTION_EXISTS(lfind HAVE_LFIND)

	CHECK_LIBRARY_EXISTS(c "" "" HAVE_LIBC)
	CHECK_LIBRARY_EXISTS(m "" "" HAVE_LIBM)

	CHECK_INCLUDE_FILES (limits.h HAVE_LIMITS_H )
	CHECK_INCLUDE_FILES (malloc.h HAVE_MALLOC_H )
	CHECK_FUNCTION_EXISTS(memmove HAVE_MEMMOVE)

	CHECK_INCLUDE_FILES (memory.h HAVE_MEMORY_H )

	CHECK_FUNCTION_EXISTS(memset HAVE_MEMSET)
	CHECK_FUNCTION_EXISTS(mmap HAVE_MMAP)
	CHECK_FUNCTION_EXISTS(pow HAVE_POW)

	#Define if you have POSIX threads libraries and header files.
	#undef HAVE_PTHREAD

	CHECK_INCLUDE_FILES (search.h HAVE_SEARCH_H )
	CHECK_FUNCTION_EXISTS(sqrt HAVE_SQRT)
	CHECK_INCLUDE_FILES (stdint.h HAVE_STDINT_H )
	CHECK_INCLUDE_FILES (stdlib.h HAVE_STDLIB_H )
	CHECK_FUNCTION_EXISTS(strcasecmp HAVE_STRCASECMP)
	CHECK_FUNCTION_EXISTS(strchr HAVE_STRCHR)
	CHECK_INCLUDE_FILES (strings.h HAVE_STRINGS_H )
	CHECK_INCLUDE_FILES (string.h HAVE_STRING_H )
	CHECK_FUNCTION_EXISTS(strrchr HAVE_STRRCHR)
	CHECK_FUNCTION_EXISTS(strstr HAVE_STRSTR)
	CHECK_FUNCTION_EXISTS(strtol HAVE_STRTOL)
	CHECK_FUNCTION_EXISTS(strtoul HAVE_STRTOUL)
	CHECK_INCLUDE_FILES ("sys/stat.h" HAVE_SYS_STAT_H )
	CHECK_INCLUDE_FILES ("sys/time.h" HAVE_SYS_TIME_H )
	CHECK_INCLUDE_FILES ("sys/types.h" HAVE_SYS_TYPES_H )
	CHECK_INCLUDE_FILES (unistd.h HAVE_UNISTD_H )
	CHECK_INCLUDE_FILES (windows.h HAVE_WINDOWS_H )

	#Native cpu byte order: 1 if big-endian (Motorola) or 0 if little-endian
	#(Intel)
	SET(HOST_BIGENDIAN 0)

	#Set the native cpu bit order (FILLORDER_LSB2MSB or FILLORDER_MSB2LSB)
	SET(HOST_FILLORDER "FILLORDER_LSB2MSB")

	SET(JPEG_SUPPORT 1)
	SET(LOGLUV_SUPPORT 1)

	#Define to the sub-directory in which libtool stores uninstalled libraries.
	#undef LT_OBJDIR

	SET(LZW_SUPPORT 1)
	SET(MDI_SUPPORT 1)
	SET(NEXT_SUPPORT 1)

	#Define to 1 if your C compiler doesn't accept -c and -o together.
	#undef NO_MINUS_C_MINUS_O

	#Support Old JPEG compresson (read contrib/ojpeg/README first! Compilationfails with unpatched IJG JPEG library)
	#undef OJPEG_SUPPORT

	SET(PACKAGE "tiff")
	SET(PACKAGE_BUGREPORT "tiff@lists.maptools.org")
	SET(PACKAGE_NAME "LibTIFF Software")
	SET(PACKAGE_STRING "LibTIFF Software 3.8.2")
	SET(PACKAGE_TARNAME "tiff")
	SET(PACKAGE_VERSION "3.8.2")
	SET(PACKBITS_SUPPORT 1)
	SET(PIXARLOG_SUPPORT 1)

	#Define to necessary symbol if this constant uses a non-standard name onyour system.
	#undef PTHREAD_CREATE_JOINABLE

	CHECK_TYPE_SIZE("int"		SIZEOF_INT)
	CHECK_TYPE_SIZE("long"		SIZEOF_LONG)

	SET(STDC_HEADERS 1)
	SET(STRIPCHOP_DEFAULT "TIFF_STRIPCHOP")
	SET(STRIP_SIZE_DEFAULT 8192)
	SET(SUBIFD_SUPPORT 1)
	SET(THUNDER_SUPPORT 1)
	SET(TIME_WITH_SYS_TIME 1)

	CHECK_SYMBOL_EXISTS("struct tm" "sys/time.h" TM_IN_SYS_TIME)
	SET(VERSION "3.8.2")

	#Define to 1 if your processor stores words with the most significant byte first (like Motorola and SPARC, unlike Intel and VAX).
	#undef WORDS_BIGENDIAN

	SET( X_DISPLAY_MISSING 1)
	SET( ZIP_SUPPORT 1)
	#Number of bits in a file offset, on hosts where this is settable.
	#undef _FILE_OFFSET_BITS

	# Define for large files, on AIX-style hosts.
	 #undef _LARGE_FILES

	# Define to empty if `const' does not conform to ANSI C.
	 #undef const

	#Define to `__inline__' or `__inline' if that's what the C compiler
	#calls it, or to nothing if 'inline' is not supported under any name.
	#ifndef __cplusplus
	#undef inline
	#endif

	#Define to `long' if <sys/types.h> does not define.
	#undef off_t

	#Define to `unsigned' if <sys/types.h> does not define.
	#undef size_t


# all is defined, so generate config.h
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/tif_config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/tif_config.h)

MESSAGE("Configure: libtiff - done.")
# end of generating tif_config.h file:

ADD_DEFINITIONS(-DHAVE_CONFIG_H )

###########################################################################################


FIND_PACKAGE(ZLIB REQUIRED)
FIND_PACKAGE(JPEG REQUIRED)

INCLUDE_DIRECTORIES( ${ZLIB_INCLUDE_DIR} ${JPEG_INCLUDE_DIR} ${CMAKE_CURRENT_BINARY_DIR})


# libtiff Library
	SET(TIFF_SRCS
		tif_aux.c
		tif_close.c
		tif_codec.c
		tif_color.c
		tif_compress.c
		tif_dir.c
		tif_dirinfo.c
		tif_dirread.c
		tif_dirwrite.c
		tif_dumpmode.c
		tif_error.c
		tif_extension.c
		tif_fax3.c
		tif_fax3sm.c
		tif_flush.c
		tif_getimage.c
		tif_jpeg.c
		tif_luv.c
		tif_lzw.c
		tif_next.c
		tif_ojpeg.c
		tif_open.c
		tif_packbits.c
		tif_pixarlog.c
		tif_predict.c
		tif_print.c
		tif_read.c
		tif_strip.c
		tif_swab.c
		tif_thunder.c
		tif_tile.c
		tif_unix.c
		tif_version.c
		tif_warning.c
		tif_write.c
		tif_zip.c)

	ADD_PREFIX("libtiff/" TIFF_SRCS)

if(NOT WIN32)
 find_library(M_LIBRARY
     NAMES m
     PATHS /usr/lib /usr/local/lib
 )
 if(NOT M_LIBRARY)
   message(STATUS
     "math library 'libm' not found - floating point support disabled")
 endif()
else()
 # not needed on windows
 set(M_LIBRARY "")
endif()
	
ADD_LIBRARY(tiff SHARED ${TIFF_SRCS})
TARGET_LINK_LIBRARIES (tiff ${ZLIB_LIBRARY} ${JPEG_LIBRARY} ${M_LIBRARY})

ADD_LIBRARY(tiffxx SHARED libtiff/tif_stream.cxx)
TARGET_LINK_LIBRARIES (tiffxx tiff)


INSTALL(TARGETS tiff tiffxx RUNTIME DESTINATION ${INSTALL_BIN} LIBRARY DESTINATION ${INSTALL_LIB} ARCHIVE DESTINATION ${INSTALL_LIB})
INSTALL(FILES libtiff/tiff.h libtiff/tiffconf.h libtiff/tiffio.h libtiff/tiffvers.h ${CMAKE_CURRENT_BINARY_DIR}/tif_config.h DESTINATION ${INSTALL_INC})

INSTALL(FILES COPYRIGHT ChangeLog README RELEASE-DATE TODO VERSION DESTINATION ${INSTALL_DATA})
INSTALL(DIRECTORY html  DESTINATION ${INSTALL_DOC})



