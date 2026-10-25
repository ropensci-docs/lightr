# Extract spectral data from spectra files

Finds and imports reflectance/transmittance/absorbance data from spectra
files in a given location.

## Usage

``` r
lr_get_spec(
  where = getwd(),
  ext = "txt",
  lim = c(300, 700),
  subdir = FALSE,
  subdir.names = FALSE,
  ignore.case = TRUE,
  interpolate = TRUE,
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

- lim:

  A vector with two numbers determining the wavelength limits to be
  considered (defaults to `c(300, 700)`).

- subdir:

  Should subdirectories within the `where` folder be included in the
  search? (defaults to `FALSE`).

- subdir.names:

  Should subdirectory path be included in the name of the spectra?
  (defaults to `FALSE`).

- ignore.case:

  Should the extension search be case insensitive? (defaults to `TRUE`)

- interpolate:

  Boolean indicated whether spectral data should be interpolated and
  pruned at every nanometre. Note that this option can only work if all
  input data samples the same wavelengths. Defaults to `TRUE`.

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

A data.frame, containing the wavelengths in the first column and
individual imported spectral files in the subsequent columns.

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
  passed to the `lr_get_spec()` function via the `...` argument.

- output: a named list of two elements, as defined in
  [`lr_parse_generic()`](https://docs.ropensci.org/lightr/reference/lr_parse_generic.md).

## See also

[`pavo::getspec()`](https://pavo.colrverse.com/reference/getspec.html)

## Examples

``` r
spcs <- lr_get_spec(system.file("testdata", package = "lightr"), ext = "jdx")
#> 1 files found; importing spectra:
head(spcs)
#>    wl OceanOptics_period
#> 1 300           154.3030
#> 2 301           129.2981
#> 3 302           115.9120
#> 4 303           122.5818
#> 5 304           125.9307
#> 6 305           152.3136
```
