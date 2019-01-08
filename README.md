Safe R Markdown Editing
=======================

When rendering R markdown to markdown formats (e.g. using the 
`github_document` output format) it is easy for people to accidentally edit 
the markdown output rather than the R markdown source.

One solution, used by `usethis::use_readme_rmd()` is to first add an HTML 
comment to the `.Rmd` source:

    <!-- README.md is generated from README.Rmd. Please edit that file -->
    
and second add a git pre-commit hook that

1. Stops a git push if `README.md` is older than `README.Rmd` (suggesting the `.Rmd` has not been compiled).

2. Stops a git push if only one of `README.md` and `README.Rmd` are staged.

These steps help to prevent mistakes, but have some disadvantages:

1. The HTML comment looks the same in both the `.Rmd` and the `.md` - as it's 
not relevant in the `.Rmd` you can get used to ignoring it.

2. Git hooks only apply locally and are not automatically added when someone 
else clones the repo. So other people working on the repo can still push by 
mistake.

This repo illustrates 3 ways to generate an HTML comment in the R markdown, such that the generating code is more naturally read as a technical detail in the source and an important comment in the output.

1. `Example_title.Rmd` includes the comment in the document title. This is probably the simplest method, but is somewhat distracting in the .`Rmd`. Adding new lines to the comment to make it stand out in the `.md` output only makes it more distracting in the `.Rmd`.

2. `Example_knit_hook.Rmd` this is probably my favoured method as R users are used to reading the **knitr** setup chunk as technical detail. You can add as many `\n` as you like to make the comment stand out in the output!

3. `Example_header.Rmd` uses `header-includes` to include the comment. This can be viewed as a compromise between the first two approaches.
