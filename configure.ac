AC_PREREQ([2.69])
AC_INIT([shell-toolbox],[2070228],[https://github.com/kusalananda/shell-toolbox/issues])

AC_CONFIG_AUX_DIR([build])

AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

AC_CONFIG_SRCDIR([src/shell.in])

# We need absolute paths for
#   * ksh93/bash (currently only used in shevil),
#   * grep, and
#   * mktemp

AC_PROG_GREP
AC_PATH_PROGS([shell_path], [ksh93 bash])
AC_PATH_PROG([mktemp_path], [mktemp])

AC_CONFIG_FILES([Makefile src/Makefile])
AC_CONFIG_FILES([src/toolbox.shlib])
AC_CONFIG_FILES([src/shell], [chmod +x src/shell])
AC_CONFIG_FILES([src/shevil], [chmod +x src/shevil])
AC_CONFIG_FILES([src/shtest], [chmod +x src/shtest])
AC_OUTPUT
