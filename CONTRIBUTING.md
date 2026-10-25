# Contributing to lightr

There are many ways you can contribute to lightr. All contributions are
very much welcome and only some of them require technical knowledge. If
you have something you would like to contribute, but you are not sure
how, please don’t hesitate to reach out by opening an
[issue](https://github.com/ropensci/lightr/issues) or sending me an
email.

## 🗣️ Spreading the word

The easiest (and possibly one of the most useful) way you can contribute
to lightr is by spreading the word. Please [cite
it](https://docs.ropensci.org/lightr/authors.html) in your publications
and tell your friends and colleagues about it!

## ✍️ Fixing typos

Small typos or grammatical errors in documentation may be edited
directly using the GitHub web interface, so long as the changes are made
in the *source* file. In other words, please edit a `.R` file in the
`R/` folder, and not the `.Rd` files in the `man/` folder. This is
because this package uses [roxygen2](https://roxygen2.r-lib.org/) to
automatically rebuild the `.Rd` files.

## 📄 Contributing test files

I am always looking for new test files but ensure that lightr works as
expected for everybody. If you have spectrometry files that you would be
willing to share, please send me an email. At the very least, I will
check if lightr parses them correctly and if they have unusual features,
I will ask you if you agree that I add them to my continuous integration
test suite (on GitHub and on CRAN).

## 😥 Reporting bugs

If you think you found a bug in lightr, even if you’re unsure, please
let me know. The best way is to open an issue on GitHub:
<https://github.com/ropensci/lightr/issues>.

Please try to create a [reprex](https://reprex.tidyverse.org/) with the
minimal amount of code required to reproduce the bug you encountered.

Please also include your session info (e.g. via the R command
[`sessioninfo::session_info()`](https://sessioninfo.r-lib.org/reference/session_info.html)).

Finally, if your issue relates to the parsing of a specific file,
remember to include said file.

## 🆕 Adding or requesting new parser

If you find a file that lightr cannot open yet, please open an issue or
send me an email with an example file. Some file formats are very
complex so I cannot guarantee that I will be able to quickly provide a
parser for all of them but I will at the very least try.

## 🗳️ Voting for new features

Whenever I can, I open a new issue with the upcoming plans for lightr.
If you are particularly interested in a specific feature and you would
like to help me prioritise my work, please use [the GitHub reactions
feature](https://github.blog/2016-03-10-add-reactions-to-pull-requests-issues-and-comments/).

## 📖 Code of Conduct

Please note that lightr is released with a [Contributor Code of
Conduct](https://ropensci.org/code-of-conduct/). By contributing to this
project you agree to abide by its terms.

# For authors and maintainers

We have a [private Google Drive shared
folder](https://drive.google.com/drive/folders/1GSGi0p4dDT7_fFJiWTJ_i_BEEvStcONE?usp=share_link)
that contains documents shared in confidence by spectrometer
manufacturers, and that we cannot make public. If you are an author and
you’d like to get access to the drive, please email the current package
maintainer (<hugo.gruson@normalesup.org>) or rOpenSci staff
(<info@ropensci.org>).
