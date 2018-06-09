dist_man1_MANS=	shell.man
dist_doc_DATA=	shell.md shell.txt
EXTRA_DIST=	shell.mdoc
DISTCLEANFILES=	shell.man shell.md shell.txt

if BUILD_MANUALS

shell.man:	$(srcdir)/shell.mdoc
	$(MANDOC) -T man -I os=Unix $(srcdir)/shell.mdoc >shell.man || true

if BUILD_MARKDOWN_MANUALS

shell.md:	$(srcdir)/shell.mdoc
	$(MANDOC) -T markdown -I os=Unix $(srcdir)/shell.mdoc >shell.md || true

endif	# BUILD_MARKDOWN_MANUALS

if BUILD_TEXT_MANUALS

shell.txt:	$(srcdir)/shell.mdoc
	$(MANDOC) -T ascii -I os=Unix $(srcdir)/shell.mdoc | \
	$(COL) -b >shell.txt || true

endif	# BUILD_TEXT_MANUALS

endif	# BUILD_MANUALS
