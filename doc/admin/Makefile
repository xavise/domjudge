ifndef TOPDIR
TOPDIR=../..
endif
include $(TOPDIR)/Makefile.global

FIGS = submitflow
FIGSPNG = $(addsuffix .png,$(FIGS))
FIGSEPS = $(addsuffix .eps,$(FIGS))

%.png: %.fig
	fig2dev -L png -m 1.4 $< $@

%.eps: %.fig
	fig2dev -L eps $< $@

docs: admin-manual.pdf admin-manual.html

install-docs: docs
	$(INSTALL_DATA) -t $(DESTDIR)$(domjudge_docdir)/admin \
		admin-manual.pdf admin-manual*.html $(FIGSPNG)

admin-manual.pdf: %.pdf: %.sgml $(TOPDIR)/doc/domjudge-overview-inc.sgml \
                                $(TOPDIR)/doc/docs_header.tex $(FIGSEPS)
# Ideally, we'd generate the pdf directly, but linuxdoc isn't able to
# include pdf figures, and the unscaled png figure looks ugly.
	linuxdoc -B latex -o ps -P "`cat $(TOPDIR)/doc/docs_header.tex`" $< >/dev/null
	ps2pdf $*.ps
	rm -f $*.ps

admin-manual.html: admin-manual.sgml $(TOPDIR)/doc/docs_header.html $(FIGSPNG)
	linuxdoc -B html --header=$(TOPDIR)/doc/docs_header.html $< >/dev/null

maintainer-clean-l:
	-rm -f $(FIGSPNG) $(FIGSEPS) admin-manual*.html admin-manual.pdf
