AC_PREREQ([2.69])
AC_INIT([shell-toolbox],[2070225])

AC_CONFIG_AUX_DIR([build])

AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

AC_CONFIG_SRCDIR([src/shell.in])

# What we need:
#   * Absolute path for ksh93/pdksh/bash, grep and mktemp

AC_PROG_GREP
AC_PATH_PROGS([shell_path], [ksh93 ksh pdksh bash])
AC_PATH_PROG([mktemp_path], [mktemp])

AC_CONFIG_FILES([Makefile src/Makefile])
AC_CONFIG_FILES([src/toolbox.fun])
AC_CONFIG_FILES([src/shell], [chmod +x src/shell])
AC_CONFIG_FILES([src/shtest], [chmod +x src/shtest])
AC_OUTPUT
