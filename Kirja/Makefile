OSAT=001_alkusanat.org \
010_johdanto.org \
020_toiminta.org \
030_toteutus.org \
taitettu_kirja.org

all: taitettu_kirja.pdf

taitettu_kirja.pdf: $(OSAT)

%_001.png: %.pdf 
	gs -dNOPAUSE -dBATCH -r160 -sDEVICE=png16m -dTextAlphaBits=4 -dGraphicsAlphaBits=4 -sOutputFile=$*_%03d.png $<

%.pdf: %.tex
	pdflatex $<

%.png: %.ink.svg
	inkscape -b '#ffffffff' -d 160 -e $@ $<

%.svg: %.ink.svg
	inkscape -l $@ $<

%.pdf: %.ink.svg
	inkscape -A $@ $<

%.eps: %.ink.svg
	inkscape -E $@ $<

%.pdf: %.org
	emacs --visit=$< --eval '(setq org-confirm-babel-evaluate nil)' -f org-latex-export-to-pdf --kill
	-$(RM) $*.tex

clean:
	-$(RM) taitettu_kirja.tex
