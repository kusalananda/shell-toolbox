dist_man1_MANS=	shell.man
EXTRA_DIST=	shell.mdoc

shell.man:	shell.mdoc
	$(mandoc) -T man -I os=Unix shell.mdoc >shell.man
