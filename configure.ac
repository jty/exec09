AC_PREREQ([2.72])
AC_INIT([m6809-run],[0.92],[brian@oddchange.com])
AC_CONFIG_SRCDIR([6809.c])
AM_INIT_AUTOMAKE([foreign])
AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_CC

# Checks for header files.
m4_warn([obsolete],
[The preprocessor macro 'STDC_HEADERS' is obsolete.
  Except in unusual embedded environments, you can safely include all
  C89 headers unconditionally.])dnl
# Autoupdate added the next two lines to ensure that your configure
# script's behavior did not change.  They are probably safe to remove.
AC_CHECK_INCLUDES_DEFAULT
AC_PROG_EGREP

AC_CHECK_HEADERS([netinet/in.h stdint.h stdlib.h string.h sys/socket.h sys/time.h termios.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_BIGENDIAN
AC_C_CONST
AC_C_INLINE
m4_warn([obsolete],
[Update your code to rely only on HAVE_SYS_TIME_H,
then remove this warning and the obsolete code below it.
All current systems provide time.h; it need not be checked for.
Not all systems provide sys/time.h, but those that do, all allow
you to include it and time.h simultaneously.])dnl
AC_CHECK_HEADERS_ONCE([sys/time.h])
# Obsolete code to be removed.
if test $ac_cv_header_sys_time_h = yes; then
  AC_DEFINE([TIME_WITH_SYS_TIME],[1],[Define to 1 if you can safely include both <sys/time.h>
	     and <time.h>.  This macro is obsolete.])
fi
# End of obsolete code.

AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT8_T
AC_C_VOLATILE

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_SELECT_ARGTYPES
m4_warn([obsolete],
[your code may safely assume C89 semantics that RETSIGTYPE is void.
Remove this warning and the 'AC_CACHE_CHECK' when you adjust the code.])dnl
AC_CACHE_CHECK([return type of signal handlers],[ac_cv_type_signal],[AC_COMPILE_IFELSE(
[AC_LANG_PROGRAM([#include <sys/types.h>
#include <signal.h>
],
		 [return *(signal (0, 0)) (0) == 1;])],
		   [ac_cv_type_signal=int],
		   [ac_cv_type_signal=void])])
AC_DEFINE_UNQUOTED([RETSIGTYPE],[$ac_cv_type_signal],[Define as the return type of signal handlers
		    ('int' or 'void').])

AC_FUNC_VPRINTF
AC_CHECK_FUNCS([gettimeofday memset select strchr strstr strtoul socket])

AC_ARG_ENABLE([wpc],
   AS_HELP_STRING([--enable-wpc],[Enable WPC address map]),
   [wpc=$enableval], [wpc=no])
if test $wpc = yes; then
   AC_DEFINE(CONFIG_WPC, 1, [Use WPC address map])
fi

AC_ARG_ENABLE([6309],
   AS_HELP_STRING([--enable-6309],[Enable 6309 extensions]),
   [h6309=$enableval], [h6309=no])
if test $h6309 = yes; then
   AC_DEFINE(H6309, 1, [Use 6309 extensions])
fi

AC_ARG_ENABLE([readline],
   AS_HELP_STRING([--enable-readline],[Enable readline library]),
   [rl_lib=$enableval], [rl_lib=no])
if test $rl_lib = yes; then
   AC_DEFINE(HAVE_READLINE, 1, [Use readline library])
	READLINE_LIBS="-L/lib -lreadline"
	AC_SUBST(READLINE_LIBS)
fi

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
