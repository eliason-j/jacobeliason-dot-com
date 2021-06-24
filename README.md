# jacobeliason-dot-com

## Attribution
This website was created using [Hugo](https://gohugo.io) and [blogdown](https://cran.r-project.org/package=blogdown). 
Special thanks to Stephen Siegerts for his `hugo-theme-basic` [template](https://github.com/siegerts/hugo-theme-basic), which I used. 
I made extensive use of Yihui Xie's [Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/) in implementing the theme and in launching the site using Github Pages.
Final acknowledgement to Zach for debugging help and general web dev consulting. 

## Workflow 

I borrow [Alison Hill's workflow](https://alison.rbind.io/blog/2020-12-new-year-new-blogdown/), which I include for my own reference here:

>1. Open the RStudio project for the site.
>2. Start the Hugo server using blogdown::serve_site() (only once due to the magic of LiveReload).
>3. View site in the RStudio viewer pane, and open in a new browser window while I work.
>4. Select existing files to edit using the file pane in RStudio.
>5. After making changes, save if a plain .md file, or if working with an .Rmd or an .Rmarkdown document, knit to preview! You can now use the Knit button to knit to the correct output format. You can also use the keyboard shortcut Cmd+Shift+K (Mac) or Ctrl+Shift+K (Windows/Linux).
>6. The console will detect the change (it will print Change detected, rebuilding site.), the viewer pane will update, and (in a few seconds) your local view in your browser will also refresh. Try to avoid hitting the refresh button in your browser.
>7. When happy with changes, add/commit/push changes to GitHub.
