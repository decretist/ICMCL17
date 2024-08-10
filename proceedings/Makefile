ICMCL17.docx: ICMCL17.md ../bib/ICMCL17.bib ../ref/proceedings.docx
	pandoc -o ICMCL17.docx --citeproc --reference-doc=../ref/proceedings.docx ICMCL17.md

ICMCL17.markdown: ICMCL17.md ../bib/ICMCL17.bib
	pandoc -o ICMCL17.markdown --citeproc -f markdown-smart -t gfm ICMCL17.md

clean:
	rm -i ICMCL17.docx

