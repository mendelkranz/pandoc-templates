## Put this Makefile in your project directory---i.e., the directory
## containing the paper you are writing. Assuming you are using the
## rest of the toolchain here, you can use it to create .docx, .tex,
## and .pdf output files (complete with bibliography, if present) from
## your markdown file.
## -    Install the `pandoc-citeproc` and `pandoc-citeproc-preamble`
##      filters for `pandoc`. See the README for links.
## -	Change the paths at the top of the file as needed.
## -	Using `make` without arguments will generate docx, tex, and pdf
## 	output files from all of the files with the designated markdown
##	extension. The default is `.md` but you can change this. 
## -	You can specify an output format with `make tex`, `make pdf`,  
## - 	`make html`, or `make docx`.
## -	Doing `make clean` will remove all the .tex, .html, .pdf, and .docx files 
## 	in your working directory. Make sure you do not have files in these
##	formats that you want to keep!


## All Rmarkdown files in the working directory
RSRC = $(wildcard *.Rmd)

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

## Pandoc options to use for all document types
OPTIONS = markdown+simple_tables+table_captions+yaml_metadata_block+smart

## MS Word template
DOCXTEMPLATE = /Users/kjhealy/.pandoc/templates/rmd-minion-reference.docx

MD=$(RSRC:.Rmd=.md)

PDFS=$(SRC:.md=.pdf)
DOCX=$(SRC:.md=.docx)
HTML=$(SRC:.md=.html)

all:	$(MD) $(PDFS) $(HTML) $(TEX) $(DOCX)

md:	clean $(MD)
pdf:	clean $(PDFS)
html:	clean $(HTML)
docx:	clean $(DOCX)

%.html:	%.md
	pandoc -w html  --template=$(PREFIX)/templates/html.template --css=$(PREFIX)/marked/kultiad-serif.css --filter pandoc-citeproc --csl=$(PREFIX)/csl/$(CSL).csl --bibliography=$(BIB) -o $@ $<


%.docx:	%.md
	pandoc -w docx --reference-doc=$(PREFIX)/templates/reference.docx  --filter pandoc-citeproc --csl=$(PREFIX)/csl/$(CSL).csl --bibliography=$(BIB) -o $@ $<

%.docx: %.md
	pandoc -r $(OPTIONS) -w docx  --filter pandoc-citeproc --csl=$(PREFIX)/csl/$(CSL).csl --bibliography=$(BIB) --reference-doc=$(DOCXTEMPLATE) -o $@ $<

%.pdf:	%.md
	pandoc -r $(OPTIONS) -s --pdf-engine=pdflatex --template=$(PREFIX)/templates/latex.template --filter pandoc-citeproc --csl=$(PREFIX)/csl/$(CSL).csl --bibliography=$(BIB) -o $@ $<


%.pdf:	%.md
	pandoc --pdf-engine=xelatex --template=$(PREFIX)/templates/article.tex --filter pandoc-citeproc --csl=$(PREFIX)/csl/$(CSL).csl --bibliography=$(BIB) -o $@ $<

clean:
	rm -f *.html *.pdf *.docx
