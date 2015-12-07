## Put this Makefile in your project directory---i.e., the directory
## containing the paper you are writing. Assuming you are using the
## rest of the toolchain here, you can use it to create .docx, .tex,
## and .pdf output files (complete with bibliography, if present) from
## your markdown file.
## -	Change the paths at the top of the file as needed.
## -	Using `make` without arguments will generate docx, tex, and pdf
## 	output files from all of the files with the designated markdown
##	extension. The default is `.md` but you can change this.
## -	You can specify an output format with `make tex`, `make pdf` or
## - 	`make docx`.
## -	Doing `make clean` will remove all the .tex, .docx, and .pdf files
## 	in your working directory. Make sure you do not have files in these
##	formats that you want to keep!

## Markdown extension (e.g. md, markdown, mdown).
MEXT = md

## All markdown files in the working directory
SRC = $(wildcard *.$(MEXT))

## Location of Pandoc support files.
PREFIX = /Users/Mendel/.pandoc

## Location of your working bibliography file
BIB = /Users/Mendel/github/papers/main.bib

## CSL stylesheet (located in the csl folder of the PREFIX directory).
CSL = chicago-fullnote-bibliography


PDFS=$(SRC:.md=.pdf)
DOCX=$(SRC:.md=.docx)
HTML=$(SRC:.md=.html)



all:	$(PDFS) $(DOCX) $(HTML)

pdf:	clean $(PDFS)
docx:	clean $(DOCX)
hmtl: clean $(HTML)

%.html:	%.md
	pandoc  -w html -S --template=$(PREFIX)/templates/html.template --css=$(PREFIX)/marked/kultiad-serif.css --filter pandoc-citeproc --csl=$(PREFIX)/csl/$(CSL).csl --bibliography=$(BIB) -o $@ $<


%.docx:	%.md
	pandoc -w docx -S -s --reference-docx=$(PREFIX)/templates/reference.docx  --filter pandoc-citeproc --csl=$(PREFIX)/csl/$(CSL).csl --bibliography=$(BIB) -o $@ $<



%.pdf:	%.md
	pandoc -s -S --latex-engine=xelatex --template=$(PREFIX)/templates/article.tex --filter pandoc-citeproc --filter pandoc-citeproc-preamble --csl=$(PREFIX)/csl/$(CSL).csl --bibliography=$(BIB) -o $@ $<

clean:
	rm -f *.docx *.pdf
