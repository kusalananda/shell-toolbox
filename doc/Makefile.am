dist_man1_MANS=	shell.man
dist_doc_DATA=	shell.md shell.txt
EXTRA_DIST=	shell.mdoc
DISTCLEANFILES=	shell.man shell.md shell.txt

shell.man:	$(srcdir)/shell.mdoc
	test -n "$(MANDOC)" && \
	$(MANDOC) -T man -I os=Unix $(srcdir)/shell.mdoc >shell.man || true

shell.md:	$(srcdir)/shell.mdoc
	test -n "$(MANDOC)" && \
	test "$(MANDOC_DOES_MARKDOWN)" -eq 1 && \
	$(MANDOC) -T markdown -I os=Unix $(srcdir)/shell.mdoc >shell.md || true

shell.txt:	$(srcdir)/shell.mdoc
	test -n "$(MANDOC)" && \
	test -n "$(COL)" && \
	$(MANDOC) -T ascii -I os=Unix $(srcdir)/shell.mdoc | \
	$(COL) -b >shell.txt || true
