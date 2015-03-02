# Process this file with autoconf to produce a configure script.

#AC_PREREQ([2.69])
AC_INIT([libbpg],
         m4_esyscmd([printf $(cat ./VERSION)]),
		[http://bellard.org/bpg/])
AC_CONFIG_SRCDIR([bpgenc.c])

AC_CONFIG_AUX_DIR([build-aux])
AM_INIT_AUTOMAKE([foreign subdir-objects])


# Checks for programs.
AC_PROG_CXX
AC_PROG_CC
LT_INIT


# Checks for libraries.
AC_CHECK_LIB([m], [sqrt], [], [exit 1])
AC_CHECK_LIB([jpeg], [jpeg_CreateCompress], [], [exit 1])
PKG_CHECK_MODULES([PNG16], [libpng16])
PKG_CHECK_MODULES([SDL], [sdl])
PKG_CHECK_MODULES([SDL_IMAGE], [SDL_image])

# x265
AC_CHECK_LIB([x265], [x265_encoder_encode], [x265="true"], [x265="false"])
AS_IF([test x$x265 = xtrue],
      [AC_ARG_ENABLE(x265,
                    AS_HELP_STRING([--enable-x265], [enable x265 support [auto]]),
                    [case "${enableval}" in
                       yes|true) x265=true ;;
                       no|false) x265=false ;;
                       *) AC_MSG_ERROR([bad value ${enableval} for --enable-x265]) ;;
                     esac],
                    [x265=$x265])
      ])
AM_CONDITIONAL([USE_X265], [test x$x265 = xtrue])

# JCTVC
AC_ARG_ENABLE(jctvc, AS_HELP_STRING([--enable-jctvc], [enable jctvc encoder [default=yes]]),
                [case "${enableval}" in
                   yes|true) jctvc=true ;;
                   no|false) jctvc=false ;;
                   *) AC_MSG_ERROR([bad value ${enableval} for --enable-jctvc]) ;;
                 esac],
                [jctvc=true])
AM_CONDITIONAL([USE_JCTVC], [test x$jctvc = xtrue])

# enable JCTVC if no encoder is enabled
jctvc_warning=""
AS_IF([test x$jctvc != xtrue -a x$x265 != xtrue],[
       jctvc=true
       jctvc_warning="WARNING: no HEVC encoder selected! JCTVC was auto-enabled"
      ])



# Checks for header files.
AC_CHECK_HEADERS([fcntl.h float.h inttypes.h limits.h malloc.h memory.h \
                  stddef.h stdint.h stdlib.h string.h unistd.h])


# Checks for typedefs, structures, and compiler characteristics.
AC_CHECK_HEADER_STDBOOL
AC_C_INLINE
AC_TYPE_INT16_T
AC_TYPE_INT32_T
AC_TYPE_INT64_T
AC_TYPE_INT8_T
AC_TYPE_SIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T
AC_CHECK_TYPES([ptrdiff_t])


# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_FUNC_STRTOD
AC_CHECK_FUNCS([floor localtime_r memchr memset pow rint sqrt strcasecmp strdup strrchr strstr strtol strtoul])


AC_CONFIG_FILES([Makefile])
AC_OUTPUT


AC_MSG_RESULT([
selected HEVC encoders:
  JCTVC: $jctvc
  x265:  $x265
$jctvc_warning])
