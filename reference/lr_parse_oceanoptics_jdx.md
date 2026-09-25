# Parse OceanOptics JCAMP-DX (.jdx) file

Parse OceanOptics/OceanInsight JCAMP-DX (.jdx) file.
<https://www.oceanoptics.com/>

## Usage

``` r
lr_parse_jdx(filename, ...)

lr_parse_oceanoptics_jdx(filename, ...)
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

'processed' column computed by lightr with the function
[`lr_compute_processed()`](https://docs.ropensci.org/lightr/reference/lr_compute_processed.md).

## References

McDonald RS, Wilks PA. JCAMP-DX: A Standard Form for Exchange of
Infrared Spectra in Computer Readable Form. Applied Spectroscopy.
1988;42(1):151-62.

## Examples

``` r
res_jdx <- lr_parse_oceanoptics_jdx(system.file("testdata", "OceanOptics_period.jdx",
                                    package = "lightr"))
head(res_jdx$data)
#>       wl      dark     white     scope processed
#> 1 176.36 32822.795 32822.795 32822.795       NaN
#> 2 176.58 32822.795 32822.795 32822.795       NaN
#> 3 176.80 32822.795 32822.795 32822.795       NaN
#> 4 177.02  1661.312  1606.017  1647.796  24.44344
#> 5 177.24  1654.349  1555.227  1660.083  -5.78479
#> 6 177.47  2568.562  2494.426  2585.356 -22.65296
res_jdx$metadata
#>  [1] "hugo" NA     NA     NA     "400"  "400"  "400"  "5"    "5"    "5"   
#> [11] "0"    "0"    "0"   
```
