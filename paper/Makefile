ICMCL17.docx: ICMCL17.md ICMCL17.bib reference.docx
	pandoc -o ICMCL17.docx --citeproc --reference-doc=reference.docx ICMCL17.md

reference.docx:
	pandoc --print-default-data-file reference.docx > reference.docx

clean:
	rm -i ICMCL17.docx

