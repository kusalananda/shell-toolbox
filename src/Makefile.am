bin_SCRIPTS=	shell
check_SCRIPTS=	t/shellcheck.test

EXTRA_DIST=	$(check_SCRIPTS)
CLEANFILES=	$(bin_SCRIPTS)

TEST_LOG_DRIVER=	env AM_TAP_AWK='$(AWK)' \
					$(SHELL) $(top_srcdir)/autotools/tap-driver.sh

TESTS=	$(check_SCRIPTS)

if !HAVE_SHELLCHECK
XFAIL_TESTS=	$(check_SCRIPTS)
endif
