# Makefile
#
# Converts Markdown to other formats (HTML, PDF, DOCX, RTF, ODT, EPUB) using Pandoc
# <http://johnmacfarlane.net/pandoc/>
#
# Run "make" (or "make all") to convert to all other formats
#
# Run "make clean" to delete converted files

# Timestamp variable
ts := $(shell /bin/date "+%y%m%d%H%M%S")

# Convert all files in this directory that have a .md suffix
SOURCE_DOCS := $(wildcard *.md)

EXPORTED_DOCS=\
 $(SOURCE_DOCS:.md=.html) \
 $(SOURCE_DOCS:.md=.pdf) \
 $(SOURCE_DOCS:.md=.docx)

# Use this syntax if you want to create pandoc files appended with timestamp

#EXPORTED_DOCS=\
# $(SOURCE_DOCS:.md=-$(ts).html) \
# $(SOURCE_DOCS:.md=-$(ts).pdf) \
# $(SOURCE_DOCS:.md=-$(ts).docx) \
# x$(SOURCE_DOCS:.md=-$(ts).rtf) \
# $(SOURCE_DOCS:.md=-$(ts).odt) \
# $(SOURCE_DOCS:.md=-$(ts).epub)

RM=/bin/rm
CP=/bin/cp

PANDOC=/usr/local/bin/pandoc

PANDOC_OPTIONS=-f markdown+smart

PANDOC_HTML_OPTIONS=--to html5
PANDOC_PDF_OPTIONS=--pdf-engine=xelatex -V geometry:margin=1.25in -V fontsize=11pt -V mainfont='Minion Pro' -V colorlinks
PANDOC_DOCX_OPTIONS=--reference-doc=pandoc-DOCX-template.docx

# Pattern-matching Rules

%.html : %.md
	cp syllabus-180H-280.md pandoc-builds/$(ts)-syllabus-180H-280.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_HTML_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

%.pdf : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_PDF_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

%.docx : %.md
	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_DOCX_OPTIONS) -o $@ $<
	cp $@ pandoc-builds/$(ts)-$@

# Recipes for timestamped files

# %-$(ts).html : %.md
# 	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_HTML_OPTIONS) -o $@ $<

# %-$(ts).pdf : %.md
# 	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_PDF_OPTIONS) -o $@ $<

# %-$(ts).docx : %.md
# 	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_DOCX_OPTIONS) -o $@ $<

# %-$(ts).rtf : %.md
# 	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_RTF_OPTIONS) -o $@ $<

# %-$(ts).odt : %.md
# 	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_ODT_OPTIONS) -o $@ $<

# %-$(ts).epub : %.md
# 	$(PANDOC) $(PANDOC_OPTIONS) $(PANDOC_EPUB_OPTIONS) -o $@ $<

# Targets and dependencies

.PHONY: all clean

all : $(EXPORTED_DOCS)

clean:
	- $(RM) $(EXPORTED_DOCS)
