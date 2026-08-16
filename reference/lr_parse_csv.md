# Parse csv files

Parse csv files

## Usage

``` r
lr_parse_csv(filename, decimal = ".", sep = ",", ...)
```

## Arguments

- filename:

  Path of the file to parse

- decimal:

  Character to be used to identify decimal plates (defaults to `.`).

- sep:

  Column delimiting characters to be considered in addition to the
  default (which are: tab, space, and ";")

- ...:

  ignored

## Value

A named list of two elements:

- `data`: a dataframe with columns "wl", "dark", "white", "scope" and
  "processed", in this order.

- `metadata`: a character vector with metadata including:

  - `user`: Name of the spectrometer operator

  - `datetime`: Timestamp of the recording in format '%Y-%m-%d %H:%M:%S'
    and UTC timezone. If timezone is missing in source file, UTC time
    will be assumed (for reproducibility purposes across computers with
    different localtimes).

  - `spec_model`: Model of the spectrometer

  - `spec_ID`: Unique ID of the spectrometer

  - `white_inttime`: Integration time of the white reference (in ms)

  - `dark_inttime`: Integration time of the dark reference (in ms)

  - `sample_inttime`: Integration time of the sample (in ms)

  - `white_avgs`: Number of averaged measurements for the white
    reference

  - `dark_avgs`: Number of averaged measurements for the dark reference

  - `sample_avgs`: Number of averaged measurements for the sample

  - `white_boxcar`: Boxcar width for the white reference

  - `dark_boxcar`: Boxcar width for the dark reference

  - `sample_boxcar`: Boxcar width for the sample reference

## Details

'processed' column computed by official software and provided as is.

## Examples

``` r
res_csv <- lr_parse_csv(
  system.file("testdata", "spec.csv", package = "lightr")
)
head(res_csv$data)
#>       wl dark white scope processed
#> 1 299.99   NA    NA    NA    10.013
#> 2 300.20   NA    NA    NA     7.331
#> 3 300.42   NA    NA    NA    12.082
#> 4 300.63   NA    NA    NA     7.949
#> 5 300.85   NA    NA    NA     5.962
#> 6 301.06   NA    NA    NA     7.525
# No metadata is extracted with this parser
res_csv$metadata
#>  [1] NA NA NA NA NA NA NA NA NA NA NA NA NA
```
