# Design Principles for lightr

This vignette outlines the design decisions that have been taken during
the development of the [lightr](https://docs.ropensci.org/lightr/) R
package, and provides some of the reasoning, and possible pros and cons
of each decision.

This document is primarily intended to be read by those interested in
understanding the code within the package and for potential package
contributors.

## Scope

This package focuses on files produced by UV/VIS spectrophotometers.

## Architecture

This package has two-level of functions:

- low-level parsers to parse spectral data and metadata from a single
  file, for which the appropriate parser is known. Users have to create
  their own loops to parse multiple files, as described in
  [`vignette("renormalise", package = "lightr")`](https://docs.ropensci.org/lightr/articles/renormalise.md).
- high-level parsers which automatically identify the relevant parser(s)
  (via the
  [`dispatch_parser()`](https://docs.ropensci.org/lightr/reference/dispatch_parser.md)
  internal function) for a collection of files and consolidate all the
  data or metadata in a single rectangular data.frame.

``` r

knitr::include_graphics("architecture.svg")
```

![The high-level functions (lr_get_spec(), lr_get_metadata() and
lr_convert_tocsv()) feed individual files to the internal dispatch
function (dispatch_parser()), which then passes each file to the
relevant low-level parser.](architecture.svg)

Package architecture diagram

## Naming conventions

- All exported functions start with the prefix `lr_`
- All low-level parsers are named as `lr_parse_<brand>_<fileext>`
