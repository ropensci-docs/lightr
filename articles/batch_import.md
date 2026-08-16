# Batch import with \`lr_get_spec()\` and \`lr_get_metadata()\`

`lightr` provides three main functions for patch import of spectral data
and metadata:

- [`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
- [`lr_get_metadata()`](https://docs.ropensci.org/lightr/reference/lr_get_metadata.md)
- [`lr_convert_tocsv()`](https://docs.ropensci.org/lightr/reference/lr_convert_tocsv.md)

Those three functions contain an internal loop and can directly be used
to import/convert whole folders.

They also allow for recursive search in the folder tree with the
argument `subdir`. In this example, the `data` that contains a
subdirectory named `procspec_files`, which contains :

    └──+ data
       ├── avantes_export.ttt
       ├── avantes_export2.trt
       ├── avantes_export_long.ttt
       └──+ procspec_files
          ├── OceanOptics_badencode.ProcSpec
          ├── OceanOptics_Linux.ProcSpec
          ├── OceanOptics_Windows.ProcSpec
          └── whiteref.ProcSpec

We first demonstrate these features on
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
but they work in the same way for
[`lr_get_metadata()`](https://docs.ropensci.org/lightr/reference/lr_get_metadata.md)
and
[`lr_convert_tocsv()`](https://docs.ropensci.org/lightr/reference/lr_convert_tocsv.md)

``` r

library(lightr)
```

## Import spectral data: `lr_get_spec()`

[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
is one the core functions of `lightr`. It finds spectral data files,
extract the reflectance / transmittance / absorbance data and returns a
`data.frame` where the first column (named `wl`) contains the
wavelengths and the subsequent columns contain the spectral data,
interpolated every nanometre:

``` r

res <- lr_get_spec(where = "data", ext = "ttt", lim = c(300, 700))
```

    ## 2 files found; importing spectra:

``` r

head(res)
```

    ##    wl avantes_export avantes_export_long
    ## 1 300         3.1487           13.624678
    ## 2 301         3.1589            5.276307
    ## 3 302         3.5700           11.023560
    ## 4 303         3.9215           10.307208
    ## 5 304         3.4034            8.980705
    ## 6 305         3.7878            8.278200

[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
also supports setting multiple file extensions at once by passing a
character vector to `ext`:

``` r

res <- lr_get_spec(where = "data", ext = c("ttt", "trt"), lim = c(300, 700))
```

    ## 3 files found; importing spectra:

    ## Warning: need at least two non-NA values to interpolate

    ## Warning: Could not import one or more files:
    ## data/avantes_export2.trt

``` r

head(res)
```

    ##    wl avantes_export avantes_export_long
    ## 1 300         3.1487           13.624678
    ## 2 301         3.1589            5.276307
    ## 3 302         3.5700           11.023560
    ## 4 303         3.9215           10.307208
    ## 5 304         3.4034            8.980705
    ## 6 305         3.7878            8.278200

Finally,
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
can also recursively search in your folder tree with the `subdir`
argument:

``` r

res <- lr_get_spec(where = "data", ext = "procspec", lim = c(300, 700), subdir = TRUE)
```

    ## 6 files found; importing spectra:

``` r

head(res)
```

    ##    wl OceanOptics_Linux OceanOptics_Windows OceanOptics_badencode  whiteref
    ## 1 300          126.5502            3.199635             -6.905214  98.30193
    ## 2 301          125.3005            3.420500             -7.034905  98.67972
    ## 3 302          127.0825            3.224495             -7.656868  98.10391
    ## 4 303          128.0483            3.320803             -8.577880 101.34410
    ## 5 304          128.9909            3.407551             -9.182934  99.86908
    ## 6 305          127.4218            3.492118             -9.367868 101.32638
    ##   BR_PF26_1 BR_PF27_3
    ## 1  19.35800  16.81450
    ## 2  19.40243  16.69849
    ## 3  19.42713  16.54195
    ## 4  19.47335  16.47455
    ## 5  19.48856  16.38495
    ## 6  19.41967  16.31837

As you may have noticed,
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
does not care about the file extension case by default. This can be
changed by using the `ignore.case` switch:

``` r

res <- lr_get_spec(where = "data", ext = "procspec", subdir = TRUE, ignore.case = FALSE)
```

    ## Warning: No files found. Try a different value for argument "ext".

If all your input files sample the wavelengths (this would be the case
if you use the same spectrometer model and same recording software), you
can also get uninterpolated data, by changing the value of the
`interpolate` boolean argument:

``` r

res <- lr_get_spec(where = file.path("data", "puffin"), ext = "procspec", interpolate = FALSE)
```

    ## 2 files found; importing spectra:

``` r

head(res)
```

    ##           wl BR_PF26_1 BR_PF27_3
    ## 570 300.2031  19.36675  16.81240
    ## 571 300.4172  19.38440  16.77861
    ## 572 300.6313  19.39979  16.73853
    ## 573 300.8454  19.38650  16.73391
    ## 574 301.0594  19.40854  16.68488
    ## 575 301.2734  19.40297  16.64210

## Import spectral metadata: `lr_get_metadata()`

[`lr_get_metadata()`](https://docs.ropensci.org/lightr/reference/lr_get_metadata.md)
extracts metadata captured by the spectrophotometer during the
recording. This metadata should be reported in your scientific articles
to ensure reproducibility of your measurements and ultimately of your
findings. The amount of information strongly depends on the brand and
model of the spectrometer.

Similarly to
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md),
it can handle multiple extensions at once and perform recursive
searches:

``` r

res <- lr_get_metadata(where = "data", ext = c("trt", "procspec"), subdir = TRUE)
```

    ## 7 files found; importing metadata:

``` r

head(res)
```

    ##                    name       user            datetime  spec_model     spec_ID
    ## 1       avantes_export2       <NA>                <NA>        <NA>   1305084U1
    ## 2     OceanOptics_Linux       hugo 2016-03-16 13:18:31     USB4000  USB4C00008
    ## 3   OceanOptics_Windows doutrelant 2015-12-04 10:29:14      JazUSB    JAZA2982
    ## 4 OceanOptics_badencode       user 2016-12-02 20:39:12 USB2000Plus USB2+H06330
    ## 5              whiteref      gomez 2018-08-02 15:56:19     USB4000  USB4C00008
    ## 6             BR_PF26_1 Adminlocal 2006-06-24 08:49:06     USB4000  USB4C00008
    ##   white_inttime dark_inttime sample_inttime white_avgs dark_avgs sample_avgs
    ## 1            95           95             95         20        20          20
    ## 2           200          200            200          5         5           5
    ## 3            60           60             60         15        15          15
    ## 4            20           20             20        100       100         100
    ## 5           500          500            500          5         5           5
    ## 6            10           10             10         40        40          40
    ##   white_boxcar dark_boxcar sample_boxcar
    ## 1            1           1             1
    ## 2            0           0             0
    ## 3            0           0             0
    ## 4            5           5             5
    ## 5            0           0             0
    ## 6           10          10            10

## Convert spectral data to csv: `lr_convert_tocsv()`

[`lr_convert_tocsv()`](https://docs.ropensci.org/lightr/reference/lr_convert_tocsv.md)
is designed for users who want an open format version for each
individual input file, possibly allowing them to carry on with their
analysis using another programming language or software.

It works in a very similar way to
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
and will create `csv` files with the same file names as the input files
(but a different extension).

``` r

lr_convert_tocsv(where = "data", ext = "procspec", subdir = TRUE)
```
