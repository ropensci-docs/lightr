# Parse OceanOptics converted file

Parse OceanOptics/OceanInsight converted file.
<https://www.oceanoptics.com/>

## Usage

``` r
lr_parse_jaz(filename, ...)

lr_parse_jazirrad(filename, ...)

lr_parse_oceanoptics_jaz(filename, ...)

lr_parse_oceanoptics_jazirrad(filename, ...)
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
res_jaz <- lr_parse_oceanoptics_jaz(system.file("testdata", "jazspec.jaz",
                        package = "lightr"))
head(res_jaz$data)
#>         wl     dark    white    scope   processed
#> 1 190.8535    0.000    0.000    0.000     0.00000
#> 2 191.2319    0.000    0.000    0.000     0.00000
#> 3 191.6103 1078.987 1156.225 1064.944   -18.18182
#> 4 191.9887 1181.970 1184.311 1062.603 -5099.91113
#> 5 192.3670 1149.203 1165.587 1074.306  -457.14148
#> 6 192.7453 1151.544 1179.630 1116.436  -125.00000
res_jaz$metadata
#>  [1] "jaz"                 "2011-08-29 16:23:13" NA                   
#>  [4] "JAZA1479"            "24"                  "24"                 
#>  [7] "24"                  "1"                   "1"                  
#> [10] "1"                   "0"                   "0"                  
#> [13] "0"                  

res_jazirrad <- lr_parse_oceanoptics_jazirrad(system.file("testdata", "irrad.JazIrrad",
                                  package = "lightr"))
head(res_jazirrad$data)
#>         wl       dark white     scope processed
#> 1 191.0163    0.00000    NA    0.0000         0
#> 2 191.3957    0.00000    NA    0.0000         0
#> 3 191.7751 -122.52458    NA -134.2367         0
#> 4 192.1545  -86.39326    NA -109.5543         0
#> 5 192.5339    0.00000    NA    0.0000         0
#> 6 192.9132  -30.52176    NA  -30.1772         0
res_jazirrad$metadata
#>  [1] "jaz"                 "2013-09-16 02:15:43" NA                   
#>  [4] "JAZA2517"            "495"                 "495"                
#>  [7] "495"                 "3"                   "3"                  
#> [10] "3"                   "5"                   "5"                  
#> [13] "5"                  

res_usb4000 <- lr_parse_oceanoptics_jaz(system.file("testdata", "OOusb4000.txt",
                            package = "lightr"))
head(res_usb4000$data)
#>       wl dark white scope processed
#> 1 178.65   NA    NA    NA     0.000
#> 2 178.86   NA    NA    NA     0.000
#> 3 179.08   NA    NA    NA     0.000
#> 4 179.30   NA    NA    NA    93.625
#> 5 179.51   NA    NA    NA    73.016
#> 6 179.73   NA    NA    NA   402.632
res_usb4000$metadata
#>  [1] "Liliane"             "2008-01-14 17:36:35" NA                   
#>  [4] "USB4A00428"          "20"                  "20"                 
#>  [7] "20"                  "50"                  "50"                 
#> [10] "50"                  "30"                  "30"                 
#> [13] "30"                 

res_transmission <- lr_parse_oceanoptics_jaz(
  system.file("testdata", "FMNH6834.00000001.Master.Transmission",
               package = "lightr")
)
head(res_transmission$data)
#>       wl dark white scope processed
#> 1 178.53   NA    NA    NA    95.380
#> 2 178.74   NA    NA    NA   675.528
#> 3 178.96   NA    NA    NA   -51.185
#> 4 179.18   NA    NA    NA     9.240
#> 5 179.39   NA    NA    NA  -417.232
#> 6 179.61   NA    NA    NA   380.121
res_transmission$metadata
#>  [1] "Valued Ocean Optics Customer" "2011-03-23 12:15:51"         
#>  [3] NA                             "USB4C01507"                  
#>  [5] "62"                           "62"                          
#>  [7] "62"                           "20"                          
#>  [9] "20"                           "20"                          
#> [11] "5"                            "5"                           
#> [13] "5"                           
```
