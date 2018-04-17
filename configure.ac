AC_PREREQ([2.69])
AC_INIT([shell-toolbox],[20180415],[https://github.com/kusalananda/shell-toolbox/issues])

AC_CONFIG_AUX_DIR([build])

AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

AC_CONFIG_SRCDIR([src/shell.in])

AC_PATH_PROG(MKTEMP, [mktemp])
AS_IF([test -z "$MKTEMP"], [AC_MSG_ERROR([mktemp is missing, can not continue])])

# Test whether "mktemp -t" adds .XXXXXXXX to the filename template or not.
# This is better than testing with "uname" in the src/shell.in script.
AC_MSG_CHECKING([whether $MKTEMP -t adds .XXXXXXXX to template])
_tmppath=$( "$MKTEMP" -t template.XXXXXXXX )
_tmpname=${_tmppath##*/}
AS_IF([test "${_tmpname#template.XXXXXXXX}" = "$_tmpname"],
      [AC_MSG_RESULT([no]); MKTEMP_TEMPLATE=".XXXXXXXX"],
      [AC_MSG_RESULT([yes]); MKTEMP_TEMPLATE=""])
rm -f "$_tmppath"
unset _tmppath _tmpname
AC_SUBST([MKTEMP_TEMPLATE])

# "mandoc" and "col" are used for generating the manuals.  These are only
# needed if the distributed manuals are ever deleted with "make distclean".
AC_PATH_PROG(MANDOC, [mandoc])
AC_PATH_PROG(COL, [col])
AS_IF([test -z "$MANDOC" || test -z "$COL"],
      [AC_MSG_WARN([mandoc and/or col is missing, manuals can not be rebuilt after "make distclean"])])

AC_CONFIG_FILES([Makefile src/Makefile doc/Makefile])
AC_CONFIG_FILES([src/shell], [chmod +x src/shell])
AC_OUTPUT
