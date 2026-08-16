# Parse SPC binary file

Parse SPC binary file. (Used by CRAIC <https://www.microspectra.com/>
and OceanOptics <https://www.oceanoptics.com/>)

## Usage

``` r
lr_parse_spc(filename, ...)

lr_parse_craic_spc(filename, ...)

lr_parse_oceanoptics_spc(filename, ...)
```

## Arguments

- filename:

  Path of the file to parse

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

## In development

Metadata parsing has not yet been implemented for this file format.

## Examples

``` r
res <- lr_parse_craic_spc(
  system.file(
    "testdata", "compare", "CRAIC", "CRAIC.spc",
    package = "lightr"
  )
)
head(res$data)
#>         wl dark white scope processed
#> 1 280.1123   NA    NA    NA  13.39989
#> 2 280.2819   NA    NA    NA  13.26464
#> 3 280.4515   NA    NA    NA  13.40967
#> 4 280.6211   NA    NA    NA  13.90005
#> 5 280.7906   NA    NA    NA  13.57364
#> 6 280.9602   NA    NA    NA  13.97229
res$metadata
#>  [1] NA                    "2012-09-28 15:47:00" NA                   
#>  [4] NA                    NA                    NA                   
#>  [7] NA                    NA                    NA                   
#> [10] NA                    NA                    NA                   
#> [13] NA                   
```
