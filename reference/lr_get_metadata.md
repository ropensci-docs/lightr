# Extract metadata from spectra files

Finds and imports metadata from spectra files in a given location.

## Usage

``` r
lr_get_metadata(
  where = getwd(),
  ext = "ProcSpec",
  subdir = FALSE,
  subdir.names = FALSE,
  ignore.case = TRUE,
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

- subdir.names:

  Should subdirectory path be included in the name of the spectra?
  (defaults to `FALSE`).

- ignore.case:

  Should the extension search be case insensitive? (defaults to `TRUE`)

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

A data.frame containing one file per row and the following columns:

- `name`: File name (without the extension)

- `user`: Name of the spectrometer operator

- `datetime`: Timestamp of the recording (ISO 8601 format)

- `spec_model`: Model of the spectrometer

- `spec_ID`: Unique ID of the spectrometer

- `white_inttime`: Integration time of the white reference (in ms)

- `dark_inttime`: Integration time of the dark reference (in ms)

- `sample_inttime`: Integration time of the sample (in ms)

- `white_avgs`: Number of averaged measurements for the white reference

- `dark_avgs`: Number of averaged measurements for the dark reference

- `sample_avgs`: Number of averaged measurements for the sample

- `white_boxcar`: Boxcar width for the white reference

- `dark_boxcar`: Boxcar width for the dark reference

- `sample_boxcar`: Boxcar width for the sample reference

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

`white_inttime`, `dark_inttime` and `sample_inttime` should be equal.
The normalised data may be inaccurate otherwise.

## References

White TE, Dalrymple RL, Noble DWA, O'Hanlon JC, Zurek DB, Umbers KDL.
Reproducible research in the study of biological coloration. Animal
Behaviour. 2015 Aug 1;106:51-7
([doi:10.1016/j.anbehav.2015.05.007](https://doi.org/10.1016/j.anbehav.2015.05.007)
).

## Examples

``` r
# \donttest{
lr_get_metadata(system.file("testdata", "procspec_files",
                            package = "lightr"),
                ext = "ProcSpec")
#> 4 files found; importing metadata:
#>                    name       user            datetime  spec_model     spec_ID
#> 1     OceanOptics_Linux       hugo 2016-03-16 13:18:31     USB4000  USB4C00008
#> 2   OceanOptics_Windows doutrelant 2015-12-04 10:29:14      JazUSB    JAZA2982
#> 3 OceanOptics_badencode       user 2016-12-02 20:39:12 USB2000Plus USB2+H06330
#> 4              whiteref      gomez 2018-08-02 15:56:19     USB4000  USB4C00008
#>   white_inttime dark_inttime sample_inttime white_avgs dark_avgs sample_avgs
#> 1           200          200            200          5         5           5
#> 2            60           60             60         15        15          15
#> 3            20           20             20        100       100         100
#> 4           500          500            500          5         5           5
#>   white_boxcar dark_boxcar sample_boxcar
#> 1            0           0             0
#> 2            0           0             0
#> 3            5           5             5
#> 4            0           0             0
# }
```
