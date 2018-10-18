#  Modifying Document Appearance

1 hour

---------------------------------------------------

The `knitr` package gives you lots of options for changing how your document looks.

## Learning Objectives

* Show how to add a table of contents and section numbering
* Modify document formatting with themes and a style sheet
* Learn how a code chunk can be integrated into a text document
* Add references to a document
* Manage sub-documents
* Include equations in your document

----------------------------------------------------
## Document Sections

We have several sections in our document; it would be nice if these were
listed in a table of contents and numbered so we could easily refer to a specific section.  We don't want to have to manually update the table of
contents or renumber everything when we move sections around; we want knitr to do as much as possible auto-magically.

In order to customize the appearance of our document, we need to pass
information to knitr about what we want.  We use the YAML header, where we customized the title and author, in order to set specific options.  

### Table of Contents

In the YAML we have a number of output formats.  You'll notice when you change
the knitr output format that the format you're interested in moves to the top
of the list.  We can make customizations to the format by removing the word
`default` after the format and including an indented list of options.  If we
want to include a table of contents, we add the option `toc: yes` to both the
`word_document` and `html_document` formats.  Then use the knit button to see
the results.

### Section Numbers and Formatting

Section numbering is where the behavior of different output formats (such as HTML versus Word) starts to diverge.
To add section numbers to our HTML document we just need to add the option
`number_sections: yes`.  We can also have the TOC appear as a document sidebar
by adding `toc_float: yes` to our options.

For the Word document, section numbering is controlled by a Word style document. Instructions for creating the Word style document are included as an optional exercise below.

## Document Themes and Custom Formatting

### HTML
The `knitr` package supports built-in themes that format the overall document. [Click
here to view available themes](https://bootswatch.com/3/). At the time of this writing, the following themes are confirmed to work with Rmarkdown and knitr: "default", "cerulean", "journal", "flatly", "readable", "spacelab", "united", "cosmo", "lumen", "paper", "sandstone", "simplex", and "yeti". 

You can control
which theme is used for the document by adding  `theme: readable` to the YAML metadata.  Try
switching our a different theme and see what happens! 

These themes are built using standard web Cascading Style Sheets (CSS).  If we don't like how any of the built in themes look, we can add a CSS style sheet to make specific changes.  In our exercise file document, the quoted text looks too big; the font is larger than the surrounding text!  We'll control this oddity with a style sheet. We've provided one for this exercise, so let's view `custom.css` in your file directory to see what it looks like. 

This style sheet edits the spacing and font size of all the quotes in the document. You can then apply this style to your
HTMl output  by adding the line `css: custom.css` to your YAML header.

### Word (_Optional step if time allows_)

You can customize Word document styling, such as fonts, sizing, and section
numbering, within the  Word program.  You can then provide `knitr` with the stylized Word document to use as a style sheet of sorts .  Because editing word document styling
is a pain, we've created a Word document with section numbering that you can use.
You just need to add `reference_docx: "Base_2013_day3_style.docx"` to the YAML
header for the `word_document` type and knit to see the result.

## Integrated Code

The benefit of using Rstudio to author reports is that you have the
ability to perform computation, live within the document.  First, let's load some
data into our exercise file.  Look at the top of the file where the DOAJ data is
imported in a code chunk.  Code chunks are demarcated by three tics \`\`\`.  The first group
of tics is followed by a label that indicates the type of code and a
description.  So, the label in this example is `{r add_dataset}`.  You'll see
RStudio makes pretty formatting around the code chunk.  There are options for
each chunk, and you can run the code by clicking the green arrow.  Then you
press the arrow, you'll notice an output message and a change in the right
'Environment' section of RStudio.  The message is the output from the
operation, and the right panel shows that the data file has been loaded.  You
can hide the output message by clicking on the up arrow or modifying the options
so that `message=FALSE`.

Let's add a new code chunk that will do something fun! At the bottom of the
'Project Description' add a new code chunk with the label `{r plot_country,echo= TRUE,fig.width=10,fig.height=11}`

Open `insert_day3a.txt` and copy the code to the body of the code chunk.

Hit the green button and you'll see a plot appear, generated by the `ggplot2` package.  When you knit the document,
this code will also execute and place a plot in the document.  

We can do the same thing to generate additional plots.  Add the code from
`insert_day3b.txt` with the
label 'plot_license' before the "Metadata" section.

## References

References are another area of document preparation where automation is really
helpful.  References in knitr are handled with BibTex files (.bib). BibTex is a
reasonably standard format that can be produced by most reference managers and
online services.  We've provided the bibliography `oajournals.bib` file for you to work with
during this course.  There is an entire section of the YAML header called `bibliography` that handles
references . You then provide knitr with the name of the
BibTex file, for example:

```
bibliography:
- oajournals.bib
``` 

Let's open our `oajournals.bib` file and see what it looks like.  You'll see
citation information about each article in groups indicated by a document type tag, e.g.,  `@article`, followed by a unique citation key (typically the last name of an author and the year of publication, e.g. Castro_2017), followed by citation information.  If you look at the exercise document, you'll note that all of the citations have thus far been written manually (e.g., Castro et al
(2017)).  We'll want to replace them by machine readable code that knitr will
be able to combine into a Reference List at the end of the report.  We use the @ symbol to indicate a
reference, so replace each reference with the appropriate tag, for example 
`@Castro_2017`. If the author's name already appears in the text, you can shorten the inline citation by placing a hyphen before the key.

At knit time, the reference list is automatically added to the end of the document under the "References" section, so we can
now delete the dummy references that were there.  

## Embedded Sub-Documents and Math

Up to now, we've been writing our report in one Rmarkdown document.  We can
actually build our document from sub-documents that knitr will integrate into
the output.  The sub-documents (aka child documents) do not have to contain a complete YAML header because they are designed to be integrated into the 'main document' or 'parent' at knit time.

To see how this works, find a document in your folder called `equations-child.Rmd`.  You
can see that this file has a minimal header followed by some
Rmarkdown text.  You'll also see some equations written in LaTeX.  That's
right; you can write LaTeX within an RMarkdown document and it will get correctly formatted at knit time.

Let's add the child document at the end of the "Project Description" section.  You
add child documents with a code chunk, and include the document location in the
label, for example: `{r equations, child = "equations-child.Rmd"}`. 

When you knit you get nicely formatted equation in both HTML and Word.

Using multiple child-documents is a convenient and tidy way to manage multiple sections in a single long report. Each section can be authored and tested seperately without bogging `knitr` down with one long scrolling document. Additionally, if just one section needs to be changed or updated over time, the parent-child authoring approach isolates the change to the necessary file without opening (and possibly introducing errors inadvertenly) to the longer parent.

Previous: [Getting Started with Markdown](01-markdown.html) Next: [Dynamic
Documents](03-dynamic.html)
