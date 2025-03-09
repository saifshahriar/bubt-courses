# Basic Makefile for LaTeX and R Markdown

# Variables
LATEX=lualatex
LATEXFLAGS=-interaction=nonstopmode -shell-escape

# Automatically find all .tex and .rmd files
TEX_SRCS := $(wildcard *.tex)
TEX_PDFS := $(TEX_SRCS:.tex=.pdf)
RMD_SRCS := $(wildcard *.rmd)
RMD_PDFS := $(RMD_SRCS:.rmd=.pdf)

# Default target builds PDFs from both LaTeX and R Markdown sources
all: clean $(TEX_PDFS) $(RMD_PDFS)

# Pattern rule for building PDFs from .tex files
%.pdf: %.tex
	$(LATEX) $(LATEXFLAGS) $<

# Pattern rule for rendering R Markdown files to PDF
%.pdf: %.rmd
	Rscript -e "rmarkdown::render('$<', output_format = 'pdf_document', output_file = '$@')"

pdf: all
	rm -f *.aux *.log *.out *.toc

# Clean auxiliary files and generated PDFs
clean:
	rm -f *.aux *.log *.out *.toc $(TEX_PDFS) $(RMD_PDFS)

.PHONY: all clean pdf
