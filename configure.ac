AC_PREREQ([2.69])
AC_INIT([shell-toolbox],[post-20180422],
        [https://github.com/kusalananda/shell-toolbox/issues])

AC_CONFIG_AUX_DIR([build])

AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

AC_CONFIG_SRCDIR([src/shell.in])

# Test whether mktemp exists, and if it does, whether "mktemp -t" adds
# .XXXXXXXX to the filename template or not.  This is better than
# testing with "uname" in the src/shell.in script.
# Note: The *minimum* number of X's on OpenBSD is six, while the
# *maximum* number of X's on Solaris is six (Solaris "mktemp -t" will
# only use the last six of the eight X's we give it here).
AC_PATH_PROG(MKTEMP, [mktemp])
AS_IF([test -n "$MKTEMP"],
      [AC_MSG_CHECKING([whether $MKTEMP -t adds .XXXXXXXX to template])
      _tmppath=$( "$MKTEMP" -t template.XXXXXXXX )
      _tmpname=${_tmppath##*/}
      AS_IF([test "${_tmpname#template.XXXXXXXX}" = "$_tmpname"],
            [AC_MSG_RESULT([no]); MKTEMP_TEMPLATE=".XXXXXXXX"],
            [AC_MSG_RESULT([yes]); MKTEMP_TEMPLATE=""])
      rm -f "$_tmppath"
      unset -v _tmppath
      unset -v _tmpname
      AC_SUBST([MKTEMP_TEMPLATE])],
      [AC_MSG_ERROR([mktemp is missing, can not continue]) ])

# mandoc is used for generating the manuals.  It's only needed if the
# distributed manuals are ever deleted (e.g. using "make distclean") or
# if the source manual sources are updated. col is used for generating
# the text-only version of the manuals.
AC_PATH_PROG(COL, [col])
AC_PATH_PROG(MANDOC, [mandoc])
AS_IF([test -n "$MANDOC"],
      [AC_MSG_CHECKING([whether $MANDOC can produce markdown output])
      AS_IF(["$MANDOC" -T markdown </dev/null 2>/dev/null],
            [MANDOC_DOES_MARKDOWN=yes],
            [MANDOC_DOES_MARKDOWN=no])
      AC_MSG_RESULT([$MANDOC_DOES_MARKDOWN])
      AC_SUBST([MANDOC_DOES_MARKDOWN])],
      [AC_MSG_WARN([mandoc is missing, manuals can not be rebuilt]) ])

AC_CONFIG_FILES([Makefile src/Makefile doc/Makefile])
AC_CONFIG_FILES([src/shell], [chmod +x src/shell])
AC_OUTPUT
