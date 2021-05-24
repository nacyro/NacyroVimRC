MDC = pandoc
MD = vi
#MDCSS = css/markdown.css
#MDCSS = css/markdown-css.css
MDCSS = css/markdown.css
MDOPTARG = --mathml --highlight-style=kate

all : $(MDCSS)
	@$(MDC) $(MD).md --from=markdown --to=html --css=$(MDCSS) $(MDOPTARG) \
		--metadata pagetitle="Vim Usage" --standalone --output=$(MD).html

.PHONY : clean
clean :
	@rm -rf ${MD}.html
