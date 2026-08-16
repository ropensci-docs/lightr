# Parse Avantes binary file

Parse Avantes binary file (TRM, ABS, ROH, DRK, REF, RAW8, RFL8 file
extensions). <https://www.avantes.com/products/spectrometers/>

## Usage

``` r
lr_parse_trm(filename, ...)

lr_parse_abs(filename, ...)

lr_parse_roh(filename, ...)

lr_parse_rfl8(filename, specnum = 1L, ...)

lr_parse_raw8(filename, specnum = 1L, ...)

lr_parse_irr8(filename, specnum = 1L, ...)

lr_parse_avantes_trm(filename, ...)

lr_parse_avantes_abs(filename, ...)

lr_parse_avantes_roh(filename, ...)

lr_parse_avantes_rfl8(filename, specnum = NULL, ...)

lr_parse_avantes_raw8(filename, specnum = NULL, ...)

lr_parse_avantes_irr8(filename, specnum = NULL, ...)
```

## Arguments

- filename:

  Path of the file to parse

- ...:

  ignored

- specnum:

  Integer representing the position of the spectrum to read in the file.
  This option only makes sense for AvaSoft8 files and is ignored in the
  other cases.

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

'processed' column computed by lightr with the function
[`lr_compute_processed()`](https://docs.ropensci.org/lightr/reference/lr_compute_processed.md).

## Examples

``` r
res_trm <- lr_parse_avantes_trm(
  system.file("testdata", "avantes_trans.TRM", package = "lightr")
)
head(res_trm$data)
#>         wl   dark  white  scope processed
#> 1 179.1006   2.40  72.50  23.65 30.313837
#> 2 179.6990  11.35 102.85  20.10  9.562842
#> 3 180.2974 -43.55  44.30 -26.75 19.123505
#> 4 180.8958 -22.15  62.55  -8.90 15.643448
#> 5 181.4942 -11.20  89.30   1.05 12.189054
#> 6 182.0925 -17.25  82.05  -6.20 11.127895
res_trm$metadata
#>  [1] NA          NA          NA          "0804016U1" "100"       "100"      
#>  [7] "100"       "20"        "20"        "20"        "0"         "0"        
#> [13] "0"        

res_roh <- lr_parse_avantes_roh(
  system.file("testdata", "avantes_reflect.ROH", package = "lightr")
)
head(res_roh$data)
#>         wl dark white    scope processed
#> 1 275.2718   NA    NA 805.0000        NA
#> 2 275.8698   NA    NA 816.3375        NA
#> 3 276.4678   NA    NA 817.1125        NA
#> 4 277.0657   NA    NA 812.4125        NA
#> 5 277.6637   NA    NA 814.3125        NA
#> 6 278.2616   NA    NA 817.6375        NA
res_roh$metadata
#>  [1] NA          NA          NA          "1305084U1" "95"        "95"       
#>  [7] "95"        "20"        "20"        "20"        "1"         "1"        
#> [13] "1"        

# This parser has a unique `specnum` argument
res_rfl8_1 <- lr_parse_avantes_rfl8(
  system.file("testdata", "compare", "Avantes", "feather.RFL8", package = "lightr"),
  specnum = 1
)
head(res_rfl8_1$data)
#>          wl      dark     white     scope processed
#> 1  995.6217 -730.5000 -155.8333 -575.1667  27.03016
#> 2 1002.5419 3427.8333 4034.8333 3589.1667  26.57883
#> 3 1009.4579 6536.5000 7168.1665 6763.1665  35.88389
#> 4 1016.3698  508.5000 1351.8334  767.8333  30.75098
#> 5 1023.2774 1193.1666 2192.5000 1529.8334  33.68913
#> 6 1030.1808  895.1667 1988.8334 1220.8334  29.77751
res_rfl8_1$metadata
#>  [1] NA                    "2016-10-06 09:40:00" NA                   
#>  [4] "1511108U1"           "639.25732421875"     "639.25732421875"    
#>  [7] "639.25732421875"     "3"                   "3"                  
#> [10] "3"                   "0"                   "0"                  
#> [13] "0"                  

res_rfl8_2 <- lr_parse_avantes_rfl8(
  system.file("testdata", "compare", "Avantes", "feather.RFL8", package = "lightr"),
  specnum = 2
)
head(res_rfl8_2$data)
#>         wl       dark    white      scope processed
#> 1 174.7803 -14.500000  2.40000 -15.000000  -2.95858
#> 2 175.3842   3.166667 14.33333  14.400000 100.59701
#> 3 175.9881   7.000000 19.76667  17.000000  78.32898
#> 4 176.5919  13.266666 21.40000  20.633333  90.57377
#> 5 177.1958  -2.666667 18.26667   3.233333  28.18471
#> 6 177.7995  19.200001 40.16667  40.933334 103.65660
res_rfl8_2$metadata
#>  [1] NA                    "2016-10-06 09:40:00" NA                   
#>  [4] "1501154U1"           "84.9001541137695"    "84.9001541137695"   
#>  [7] "84.9001541137695"    "10"                  "10"                 
#> [10] "10"                  "1"                   "1"                  
#> [13] "1"                  
```
