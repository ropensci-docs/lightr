# Parse OceanOptics ProcSpec file

Parse OceanOptics/OceanInsight ProcSpec file.
<https://www.oceanoptics.com/>

## Usage

``` r
lr_parse_procspec(filename, verify_checksum = FALSE, ...)

lr_parse_oceanoptics_procspec(filename, verify_checksum = FALSE, ...)
```

## Arguments

- filename:

  Path of the file to parse

- verify_checksum:

  Logical (defaults to `FALSE`). Should we check if the file has been
  modified since its creation by the spectrometer? An error will be
  returned if the check fails.

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

## References

<https://www.oceanoptics.com/software/>

## Examples

``` r
res <- lr_parse_oceanoptics_procspec(system.file("testdata", "procspec_files",
                                     "OceanOptics_Linux.ProcSpec",
                                     package = "lightr"),
                         verify_checksum = TRUE)
head(res$data)
#>         wl      dark     white     scope processed
#> 1 176.3604 32822.795 32822.795 32822.795   0.00000
#> 2 176.5816 32822.795 32822.795 32822.795   0.00000
#> 3 176.8027 32822.795 32822.795 32822.795   0.00000
#> 4 177.0238  1483.549  1517.545  1496.656  38.55422
#> 5 177.2449  1492.150  1506.486  1510.991 131.42857
#> 6 177.4660  1965.640  1934.102  1976.290 -33.76623
res$metadata
#>  [1] "hugo"                "2016-03-16 13:18:31" "USB4000"            
#>  [4] "USB4C00008"          "200"                 "200"                
#>  [7] "200"                 "5"                   "5"                  
#> [10] "5"                   "0"                   "0"                  
#> [13] "0"                  
```
