bin_SCRIPTS=	src/shell
dist_man1_MANS=	doc/shell.man

dist_doc_DATA=	\
	LICENSE NEWS README \
	doc/shell.txt

check_scripts_src=	t/shellcheck.test
check_scripts_doc=	t/mandoc-lint.test
check_SCRIPTS=	$(check_scripts_src) $(check_scripts_doc)

EXTRA_DIST=	\
	doc/shell.mdoc \
	$(check_SCRIPTS)

CLEANFILES=	$(bin_SCRIPTS)
DISTCLEANFILES=	doc/shell.man doc/shell.txt

TEST_LOG_DRIVER=	\
	env AM_TAP_AWK='$(AWK)' \
	$(SHELL) $(top_srcdir)/autotools/tap-driver.sh

TESTS=	$(check_SCRIPTS)

XFAIL_TESTS=

if !HAVE_SHELLCHECK
XFAIL_TESTS+=    $(check_scripts_src)
endif

if !HAVE_MANDOC
XFAIL_TESTS+=	$(check_scripts_doc)

$(dist_man1_MANS) $(dist_doc_DATA):
	@echo 'You lack the mandoc utility. Can not rebuild manuals.' >&2
	@exit 1

else

SUFFIXES=	.mdoc .man .txt

.mdoc.man:
	$(MANDOC) -T man -I os=Unix $< >$@ || true

.mdoc.txt:
	$(MANDOC) -T ascii -I os=Unix $< | \
	$(COL) -b >$@ || true

doc/shell.man doc/shell.txt:	doc/shell.mdoc

endif	# !HAVE_MANDOC
