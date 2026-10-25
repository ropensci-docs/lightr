# Convert spectral data files to csv files

Convert spectral data files to csv files

## Usage

``` r
lr_convert_tocsv(
  where = NULL,
  ext = "txt",
  subdir = FALSE,
  ignore.case = TRUE,
  overwrite = FALSE,
  metadata = TRUE,
  parser = NULL,
  ...
)
```

## Arguments

- where:

  Folder in which files are located (defaults to current working
  directory).

- ext:

  File extension to be searched for, without the "." (defaults to
  `txt`). You can also use a character vector to specify multiple file
  extensions.

- subdir:

  Should subdirectories within the `where` folder be included in the
  search? (defaults to `FALSE`).

- ignore.case:

  Should the extension search be case insensitive? (defaults to `TRUE`)

- overwrite:

  logical. Should the function overwrite existing files with the same
  name? (defaults to `FALSE`).

- metadata:

  logical (defaults to `TRUE`). Should metadata be exported as well?
  They will be exported in csv files will the `_metadata.csv` suffix.

- parser:

  Optional function to specify the parser to be used. By default, the
  parser is automatically selected based on the file extension. This
  argument can be used to force the use of a specific parser, or to pass
  a custom parser. See details for more information on custom parsers.
  Please note that this argument can produce easily produce invalid
  results if used incorrectly and only advanced users should use it,
  with extra caution.

- ...:

  Arguments passed to individual parsers.

## Value

Convert input files to csv and invisibly return the list of created file
paths

## Details

### Parallel processing

You can customise the type of parallel processing used by this function
with the
[`future::plan()`](https://future.futureverse.org/reference/plan.html)
function. This works on all operating systems, as well as high
performance computing (HPC) environment. Similarly, you can customise
the way progress is shown with the
[`progressr::handlers()`](https://progressr.futureverse.org/reference/handlers.html)
functions (progress bar, acoustic feedback, nothing, etc.)

### Custom parsers

To create a custom parser to pass to the `parser` argument, you need to
create with the following signature:

- input: a file path (string) as a first argument, and optionally, any
  additional arguments needed to parse the file. These arguments can be
  passed to the
  [`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
  function via the `...` argument.

- output: a named list of two elements, as defined in
  [`lr_parse_generic()`](https://docs.ropensci.org/lightr/reference/lr_parse_generic.md).

## Warning

When `metadata = TRUE`, if **either** the data **or** metadata export
fails, nothing will be returned for this file.
