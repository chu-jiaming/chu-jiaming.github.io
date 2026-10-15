# Build the resumes with XeLaTeX via latexmk (settings in .latexmkrc).
#
#   make          build both PDFs into build/
#   make zh       Chinese only (build/resume-zh.pdf)
#   make en       English only (build/resume-en.pdf)
#   make watch    rebuild both on every save
#   make publish  build phone-free copies for the website (cv/resume-*.pdf)
#   make clean    remove auxiliary files, keep the PDFs
#   make distclean  remove build/ entirely

LATEXMK := latexmk
FLAGS   := -interaction=nonstopmode -halt-on-error
DEPS    := resume.cls .latexmkrc $(wildcard private.tex)

.PHONY: all zh en watch publish clean distclean

all: zh en

zh: build/resume-zh.pdf
en: build/resume-en.pdf

build/%.pdf: %.tex $(DEPS)
	$(LATEXMK) $(FLAGS) $<

watch:
	$(LATEXMK) $(FLAGS) -pvc -view=none resume-zh.tex resume-en.tex

# Public PDFs are committed next to the sources and linked from index.html.
# \publicbuild hides the phone number even when private.tex exists.
publish: resume-zh.tex resume-en.tex $(DEPS)
	$(LATEXMK) $(FLAGS) -outdir=build/public -usepretex='\def\publicbuild{}' resume-zh.tex resume-en.tex
	cp build/public/resume-zh.pdf build/public/resume-en.pdf .

clean:
	$(LATEXMK) -c resume-zh.tex resume-en.tex

distclean:
	rm -rf build
