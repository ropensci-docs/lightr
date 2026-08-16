# Parse Avantes converted file

Parse Avantes converted file.
<https://www.avantes.com/products/spectrometers/>

## Usage

``` r
lr_parse_ttt(filename, ...)

lr_parse_trt(filename, ...)

lr_parse_avantes_ttt(filename, ...)

lr_parse_avantes_trt(filename, ...)
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

## Examples

``` r
res_ttt <- lr_parse_avantes_ttt(
  system.file("testdata", "avantes_export.ttt", package = "lightr")
)
head(res_ttt$data)
#>    wl dark white scope processed
#> 1 300   NA    NA    NA    3.1487
#> 2 301   NA    NA    NA    3.1589
#> 3 302   NA    NA    NA    3.5700
#> 4 303   NA    NA    NA    3.9215
#> 5 304   NA    NA    NA    3.4034
#> 6 305   NA    NA    NA    3.7878
res_ttt$metadata
#>  [1] NA          NA          NA          "0804016U1" "100.00"    "100.00"   
#>  [7] "100.00"    "20"        "20"        "20"        "0"         "0"        
#> [13] "0"        

res_trt <- lr_parse_avantes_trt(
  system.file("testdata", "avantes_export2.trt", package = "lightr")
)
head(res_trt$data)
#>       wl dark white  scope processed
#> 1 275.27   NA    NA 805.00        NA
#> 2 275.87   NA    NA 816.34        NA
#> 3 276.47   NA    NA 817.11        NA
#> 4 277.07   NA    NA 812.41        NA
#> 5 277.66   NA    NA 814.31        NA
#> 6 278.26   NA    NA 817.64        NA
res_trt$metadata
#>  [1] NA          NA          NA          "1305084U1" "95.00"     "95.00"    
#>  [7] "95.00"     "20"        "20"        "20"        "1"         "1"        
#> [13] "1"        
```
