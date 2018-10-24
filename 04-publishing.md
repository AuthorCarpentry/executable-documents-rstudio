#  Publishing Your Reproducible Report

1.5 hours

---------------------------------------------------

## Learning Objectives

* Publish your document and code via GitHub and, if time, RStudio


### GitHub

In your GitHub account, create a new repository (the
name doesn't matter) and make sure to check the box for Initialize this repo
with a README file.  Open Finder of Windows explorer on your computer.
Navigate to the data directory and find the .html file you've been knitting.
Rename this file to `index.html`.  

On GitHub, click on 'Upload a file'. Drag
index.html  to the box and click the green button at the bottom.  Now go to
settings on GitHub.  Scroll down to the GHPages section and click the dropbown
to select masster.  Click Save.  If you now scroll down to the GHPages section
you'll see a github.io url.  Copy this and go back to the code section of your GitHub Repository.  Click and add the url.  If you click on this link you'll see your report!

### Rpubs

Open your document in Rstudio.  Click Knit.  You'll see a publish button in the
item view pane - click it.  You'll be redirected to the rpubs web site.  If you
don't have an account you'll need to register.  You'll see a screen with basic
metadata, but all is optional.  Your document is published online!

### Binder

We need to copy all files used by knitter into our GitHub repository.  Make a
copy of your .Rmd file that doesn't include the ORCID section (The
authentication is a pain).  Then we
need to tell Binder that we want to run R and what our dependencies are.  In
GitHub, create a `runtime.txt` file that contains: `r-2018-07-09`.  This
chooses a version of R at the date indicated.  Next create a `install.R` file
that contains:

```
install.packages("rmarkdown")
install.packages("bitops")
install.packages("caTools")
install.packages("tidyverse")
install.packages("DT")
```
Now edit the README file in Github and add:

```
https://mybinder.org/v2/gh/AuthorCarpentry/R-Binder/master?urlpath=rstudio
```

replacing `AuthorCarpentry` with your GitHub account name and `R-Binder` with
your GitHub repository name.  Click the Binder button and your environment will
load (it might take up to 20 mins the first time).

## Wrapup

