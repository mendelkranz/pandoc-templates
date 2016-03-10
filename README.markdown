# Pandoc Configuration and Support Files

## Description

A collection of support files for use with Pandoc, and specifically for helping to turn pandoc markdown files into nice HTML, LaTeX, and PDF output. These files go in your `~/.pandoc/` folder. Some files are designed to work with the style and configuration material provided in [latex-custom-kjh](http://kjhealy.github.com/latex-custom-kjh/).

## Notes

What's included?

- A fork of the default [pandoc](http://johnmacfarlane.net/pandoc/) templates. These go in
`~/.pandoc/templates`. These can be be pointed to directly with the
`--template=` switch as appropriate.
- I preview markdown files using
  [Marked](http://marked2app.com/), a very handy live previewer
  for markdown files. The `css` files in the `marked/` folder are
  meant to be used together with pandoc and
  [Marked](http://markedapp.com/). You point Marked to use pandoc in Marked >
  Preferences > Advanced. Then specify the file Path to Pandoc. With the new mactex version for 2015 my file path looks like this `/usr/local/bin/pandoc`You can add the various switches and arguments to pandoc
  in the 'Args' field below it, mine look like this:

    ```
    -r markdown -w html -s -S --filter pandoc-citeproc
    --bibliography=/Users/Mendel/github/papers/main.bib
    --csl=/Users/Mendel/.pandoc/csl/chicago-fullnote-bibliography.csl
    ```

    Then check the box telling Marked to use this by default. Note
    that you may have to specify the path to any pandoc filters you
    use.
- The CSS files can be added in Marked > Style > Custom CSS. Marked
  can then use them to format the HTML output.
- The CSL files in the `csl/` folder format the bibliography generated
  by pandoc and citeproc. The `chicago-syllabus.csl` file makes a
  tiny change to a standard Chicago Notes CSL file so you can use it
  to output citation information in the body text of a document. This
  makes it useful for lists of references in CVs and course
  syllabuses.
- The Makefile in the `makefile/` folder helps you generate HTML, DOCX, and PDF output from your markdown files in a convenient
  way. It is meant to go in the folder where you are writing your
  paper. It looks for `.md` files in the working directory and
  converts them to nice HTML, PDF, and DOCX. You can of course
  change the bibliography and template files as desired.
- The `pandoc` commands produced by the current version of the `Makefile` include switches that invoke a [pandoc filters](http://pandoc.org/scripting.html) that does additional processing on the bibliography and cross-references in the document. You should install [pandoc-citeproc-preamble](https://github.com/spwhitton/pandoc-citeproc-preamble) to make it work.