AC_PREREQ([2.69])
AC_INIT([shell-toolbox],[20190528+],[https://github.com/kusalananda/shell-toolbox/issues])

AC_CONFIG_AUX_DIR([autotools])

AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE

AC_REQUIRE_AUX_FILE([tap-driver.sh])
AC_CONFIG_SRCDIR([src/shell.in])

# The following allows a user to override what sh we use in the #!-lines
# of the scripts.
AC_PATH_PROG(SH, [sh])

# OpenBSD sh(1) and ksh(1) has a wierd behaviour that allows
#   eval false || true
# to terminate the shell if running with the errexit shell option set
# (which these scripts do), even though it's an AND-OR list.  Test this
# for the $SH found above.
# See https://unix.stackexchange.com/questions/523098 and
#     https://marc.info/?l=openbsd-misc&m=155975799609668
AC_MSG_CHECKING([for faulty eval if errexit is set])
AS_IF([$SH -e -c 'eval false || true'],
      [AC_MSG_RESULT([no])],
      [AC_MSG_RESULT([yes])
       AC_MSG_ERROR(
[$SH is not usable, consider selecting another shell \
using SH=/path/to/shell as an argument to the configure script]) ])

# Test whether mktemp exists, and if it does, whether "mktemp -t" adds
# .XXXXXXXX to the filename template or not.
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
      AS_UNSET([_tmppath])
      AS_UNSET([_tmpname])
      AC_SUBST([MKTEMP_TEMPLATE])],
      [AC_MSG_ERROR([mktemp is missing, can not continue]) ])

# mandoc is used for generating the manuals and in the doc "check"
# target.  It's only needed if the distributed manuals are ever deleted
# (e.g. using "make distclean") or if the source manual sources are
# updated. col is used for generating the text-only version of the
# manuals.
AC_PATH_PROG(MANDOC, [mandoc])
AC_PATH_PROG(COL, [col])
AM_CONDITIONAL([HAVE_MANDOC], [test -n "$MANDOC" && test -n "$COL"])

AM_COND_IF([HAVE_MANDOC],
      [AC_MSG_CHECKING([whether $MANDOC can produce markdown output])
      AM_CONDITIONAL([HAVE_MANDOC],
                     ["$MANDOC" -T markdown </dev/null 2>/dev/null])
      AM_COND_IF([HAVE_MANDOC],
                 [AC_MSG_RESULT([yes])],
                 [AC_MSG_RESULT([no])]) ])

AM_COND_IF([HAVE_MANDOC], [],
      [AC_MSG_WARN([col or usable mandoc is missing, manuals can not be rebuilt])
       AC_MSG_WARN([mandoc is missing, "make check" disabled for documentation])])

# shellcheck is only used in the src "check" target.
AC_PATH_PROG(SHELLCHECK, [shellcheck])
AM_CONDITIONAL([HAVE_SHELLCHECK], [test -n "$SHELLCHECK"])

AM_COND_IF([HAVE_SHELLCHECK], [],
    [AC_MSG_WARN([shellcheck is missing, "make check" disabled for source])])

# Test whether we should use pax or cp to copy directories.
AC_PATH_PROGS(PAX, [pax cp])
AS_IF([test -z "$PAX"],
      [AC_MSG_ERROR([Did not find pax nor cp])])

AC_CONFIG_FILES([Makefile src/Makefile doc/Makefile])
AC_CONFIG_FILES([src/shell], [chmod +x src/shell])
AC_CONFIG_FILES([src/shell-common.shlib])
AC_OUTPUT
