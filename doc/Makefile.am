dist_man1_MANS=	shell.man
dist_doc_DATA=	shell.md shell.txt
check_SCRIPTS=	t/mandoc-lint.test

EXTRA_DIST=	shell.mdoc \
			$(check_SCRIPTS)
DISTCLEANFILES=	shell.man shell.md shell.txt

if !HAVE_MANDOC

$(dist_man1_MANS) $(dist_doc_DATA):
	@echo 'You lack the mandoc utility. Can not rebuild manuals.' >&2
	@exit 1

check:
	@echo 'You lack the mandoc utility. Documentation checks disabled.' >&2
	@exit

else

shell.man:	$(srcdir)/shell.mdoc
	$(MANDOC) -T man -I os=Unix $(srcdir)/shell.mdoc >shell.man || true

shell.md:	$(srcdir)/shell.mdoc
	$(MANDOC) -T markdown -I os=Unix $(srcdir)/shell.mdoc >shell.md || true

shell.txt:	$(srcdir)/shell.mdoc
	$(MANDOC) -T ascii -I os=Unix  $(srcdir)/shell.mdoc | \
	$(COL) -b >shell.txt || true

TEST_LOG_DRIVER=	env AM_TAP_AWK='$(AWK)' \
					$(SHELL) $(top_srcdir)/autotools/tap-driver.sh

TESTS=	$(check_SCRIPTS)

endif	# !HAVE_MANDOC

