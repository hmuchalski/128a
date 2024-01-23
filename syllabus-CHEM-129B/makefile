# Makefile for conversion of a Markdown input file
# to other formats (HTML, PDF, DOCX, RTF, ODT, EPUB) using Pandoc
# <http://johnmacfarlane.net/pandoc/>
#
# The input file is converted using PANDOC_OPTIONS.
# Then, the output file is copied to "pandoc-builds" directory with a timestamp as a prefix
#
# Run "make pdf" to only execute conversion to PDF etc.
# Run "make all" to convert to formats listed under EXPORTED_DOCS
# Run "make clean" to delete converted files (it doesn't delete files in "pandoc-builds" directory)

# Defining the timestamp variable
ts := $(shell /bin/date "+%y%m%d%H%M")

# Semester variable
SEMESTER=ay-23-24-spring

# Convert all files in this directory that have a .md suffix
SOURCE_DOCS := $(wildcard *.md)

# Create pandoc files appended with semester name

EXPORTED_DOCS=\
 $(SOURCE_DOCS:.md=-$(SEMESTER).txt) \
 $(SOURCE_DOCS:.md=-$(SEMESTER).html) \
 $(SOURCE_DOCS:.md=-standalone.html) \
 $(SOURCE_DOCS:.md=-$(SEMESTER).tex) \
 $(SOURCE_DOCS:.md=-$(SEMESTER).pdf) \
 $(SOURCE_DOCS:.md=-toc-$(SEMESTER).pdf) \
 $(SOURCE_DOCS:.md=-$(SEMESTER)-test.pdf) \
 $(SOURCE_DOCS:.md=-$(SEMESTER).docx)\
 $(SOURCE_DOCS:.md=-$(SEMESTER)-calibri.docx)

PUBLISHED_DOCS=\
 $(SOURCE_DOCS:.md=-$(SEMESTER).pdf) \
 $(SOURCE_DOCS:.md=-toc-$(SEMESTER).pdf) \
 $(SOURCE_DOCS:.md=-$(SEMESTER).docx)\
 $(SOURCE_DOCS:.md=-$(SEMESTER)-calibri.docx)


# Define commands

RM=/bin/rm
CP=/bin/cp
PANDOC=/usr/local/bin/pandoc

# Pandoc

PANDOC_OPTIONS=-f markdown+smart

PANDOC_MD_OPTIONS=-t markdown
PANDOC_HTML_OPTIONS=--to html5
PANDOC_STANDALONE_HTML_OPTIONS=--to html5 -s --toc
PANDOC_LATEX_OPTIONS=-t latex
PANDOC_TOC_PDF_OPTIONS=--pdf-engine=xelatex -V geometry:margin=1.25in -V fontsize=11pt -V mainfont='Minion Pro' -V colorlinks --toc --toc-depth=1
PANDOC_PDF_OPTIONS=--pdf-engine=xelatex -V geometry:margin=1.25in -V fontsize=11pt -V mainfont='Minion Pro' -V colorlinks
PANDOC_DOCX_OPTIONS=--reference-doc=/Users/hmuchalski-local/.pandoc/templates/pandoc-DOCX-template.docx
PANDOC_DOCX_CALIBRI_OPTIONS=--reference-doc=/Users/hmuchalski-local/.pandoc/templates/pandoc-DOCX-template-calibri.docx


# Pattern-matching rules. The "md" rule is for achiving purposes

%-$(SEMESTER).txt : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_MD_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

%-$(SEMESTER).html : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_HTML_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

%-standalone.html : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_STANDALONE_HTML_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

%-$(SEMESTER).tex : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_PDF_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

%-$(SEMESTER).pdf : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_PDF_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@
	cp $@ ../_current_$@

%-toc-$(SEMESTER).pdf : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_TOC_PDF_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

%-$(SEMESTER)-test.pdf : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_PDF_OPTIONS) -o $@ $<

%-$(SEMESTER).docx : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_DOCX_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

%-$(SEMESTER)-calibri.docx : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_DOCX_CALIBRI_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@


%-$(SEMESTER)-test.docx : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_DOCX_OPTIONS) -o $@ $<

# Targets and dependencies

.PHONY: all clean

all : $(EXPORTED_DOCS)
print: $(PUBLISHED_DOCS)

# Individual outputs commands

md : $(SOURCE_DOCS:.md=-$(SEMESTER).txt)
standalone : $(SOURCE_DOCS:.md=-standalone.html)
html : $(SOURCE_DOCS:.md=-$(SEMESTER).html)
latex : $(SOURCE_DOCS:.md=-$(SEMESTER).tex)
test : $(SOURCE_DOCS:.md=-$(SEMESTER)-test.pdf)
test-docx : $(SOURCE_DOCS:.md=-$(SEMESTER)-test.docx)	
pdf-toc : $(SOURCE_DOCS:.md=-toc-$(SEMESTER).pdf)
pdf : $(SOURCE_DOCS:.md=-$(SEMESTER).pdf)	
docx : $(SOURCE_DOCS:.md=-$(SEMESTER).docx)
docx-calibri : $(SOURCE_DOCS:.md=-$(SEMESTER)-calibri.docx)

clean:
	- $(RM) $(EXPORTED_DOCS)
