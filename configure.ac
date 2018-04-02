AC_PREREQ([2.69])
AC_INIT([shell-toolbox],[20180401],[https://github.com/kusalananda/shell-toolbox/issues])

AC_CONFIG_AUX_DIR([build])

AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

AC_CONFIG_SRCDIR([src/shell.in])

# "mandoc" and "col" are used for generating the manuals.  These are only
# needed if the distributed manuals are deleted with "make distclean".
AC_PATH_PROG(MANDOC, [mandoc])
AC_PATH_PROG(COL, [col])
AS_IF([test -z "$MANDOC" || test -z "$COL"],
      [AC_MSG_WARN([mandoc and/or col is missing, manuals can not be rebuilt after "make distclean"])])

AC_CONFIG_FILES([Makefile src/Makefile doc/Makefile])
AC_CONFIG_FILES([src/shell], [chmod +x src/shell])
AC_OUTPUT
