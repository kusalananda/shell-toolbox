dist_man1_MANS=	shell.man
dist_doc_DATA=	shell.md shell.txt
EXTRA_DIST=	shell.mdoc
DISTCLEANFILES=	shell.man shell.md shell.txt

shell.man:	$(srcdir)/shell.mdoc
	$(mandoc) -T man -I os=Unix $(srcdir)/shell.mdoc >shell.man

shell.md:	$(srcdir)/shell.mdoc
	$(mandoc) -T markdown -I os=Unix $(srcdir)/shell.mdoc >shell.md

shell.txt:	$(srcdir)/shell.mdoc
	$(mandoc) -I os=Unix $(srcdir)/shell.mdoc >shell.txt
