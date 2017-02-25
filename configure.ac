AC_PREREQ([2.69])
AC_INIT([shell-toolbox],[2070225])

AC_CONFIG_AUX_DIR([build])

AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

AC_CONFIG_SRCDIR([src/shell.in])

# We need KornShell or bash
AC_PATH_PROGS([shell_path], [ksh93 bash])

# TODO: Fail if neither ksh93 nor bash was found

# We need grep
AC_PROG_GREP

# We need mktemp
AC_PATH_PROG([mktemp_path], [mktemp])

# TODO: Make sure mktemp supports -d and -p

AC_CONFIG_FILES([Makefile src/Makefile])
AC_CONFIG_FILES([src/shell], [chmod +x src/shell])
AC_CONFIG_FILES([src/shtest], [chmod +x src/shtest])
AC_OUTPUT
