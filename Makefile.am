ACLOCAL_AMFLAGS = -I m4

SUBDIRS = source

pkgconfiglibdir   = $(libdir)/pkgconfig
pkgconfiglib_DATA = libbpg.pc

doc_DATA  = ChangeLog README doc/bpg_spec.txt
man1_MANS = man/bpgdec.1 man/bpgenc.1 man/bpgmux.1 man/bpgview.1
man5_MANS = man/bpg.5

CLEANFILES = $(man1_MANS) $(man5_MANS)


make_man1 = \
	cat man/templates/$^.1.header > $@ ; \
	source/$^ >> $@ || true ; \
	cat man/templates/$^.1.footer >> $@

man/bpgdec.1: bpgdec
	$(make_man1)

man/bpgenc.1: bpgenc
	$(make_man1)

man/bpgmux.1: bpgmux
	$(make_man1)

man/bpgview.1: bpgview
	$(make_man1)

man/bpg.5:
	cat man/templates/bpg.5.header > $@
	cat doc/bpg_spec.txt >> $@
	cat man/templates/bpg.5.footer >> $@


bpgdec bpgenc bpgmux bpgview libbpg.la javascripts bpgdec.js bpgdec8.js bpgdec8a.js:
	$(MAKE) -C source $@

