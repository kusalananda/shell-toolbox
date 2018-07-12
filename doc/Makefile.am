dist_man1_MANS=	shell.man
dist_doc_DATA=	shell.md shell.txt
EXTRA_DIST=	shell.mdoc
DISTCLEANFILES=	shell.man shell.md shell.txt

if !BUILD_MANUALS
all:
	echo 'You lack the mandoc utility' >&2
	echo 'Can not rebuild manuals' >&2
	exit 1

else

shell.man:	$(srcdir)/shell.mdoc
	$(MANDOC) -T man -I os=Unix $(srcdir)/shell.mdoc >shell.man || true

shell.md:	$(srcdir)/shell.mdoc
	$(MANDOC) -T markdown -I os=Unix $(srcdir)/shell.mdoc >shell.md || true

shell.txt:	$(srcdir)/shell.mdoc
	$(MANDOC) -T ascii -I os=Unix $(srcdir)/shell.mdoc | \
	$(COL) -b >shell.txt || true

endif	# BUILD_MANUALS
