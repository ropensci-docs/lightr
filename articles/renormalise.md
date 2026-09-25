# Renormalise spectral data with a custom reference

Some use cases require more flexibility than the high-level
user-friendly functions provides by `lightr`. For this use case,
`lightr` also exports the low-level individual parsers, which allow the
user to code its own custom workflow.

We don’t recommend the use of those functions unless you absolutely have
to. Most users should use
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
and
[`lr_get_metadata()`](https://docs.ropensci.org/lightr/reference/lr_get_metadata.md)
instead.

Here, we take the example of the method presented in Gruson et al.
(2019) where reflectance spectra need to be normalised in an unusual
way.

Raw, un-normalised spectral data depends on both the spectrometer and
the lamp as well as the conditions during the recording (including
ambient light, temperature, *etc*.). To allow for comparison between
studies, it is thus normalised by a white and a dark reference with the
following formula:

``` math
\dfrac{\text{Raw} - \text{Dark}}{\text{White} - \text{Dark}}
```

For this example here, we need to normalise the raw data by a white
reference contained in another file. This can’t be done with with
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
because
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
returns reflectance spectra that have already been normalised by the
white reference contained in the same file.

``` r

library(lightr)
```

## Step 1: import un-normalised data

We manually import the data using the appropriate low-level parser:

``` r

reflect_data <- lr_parse_oceanoptics_procspec(
  system.file("testdata", "procspec_files", "OceanOptics_Linux.ProcSpec",
               package = "lightr")
  )
length(reflect_data)
```

    ## [1] 2

The result contains 2 elements:

- the spectral data itself
- the metadata captured during the recording

``` r

head(reflect_data[[1]])
```

    ##         wl      dark     white     scope processed
    ## 1 176.3604 32822.795 32822.795 32822.795   0.00000
    ## 2 176.5816 32822.795 32822.795 32822.795   0.00000
    ## 3 176.8027 32822.795 32822.795 32822.795   0.00000
    ## 4 177.0238  1483.549  1517.545  1496.656  38.55422
    ## 5 177.2449  1492.150  1506.486  1510.991 131.42857
    ## 6 177.4660  1965.640  1934.102  1976.290 -33.76623

## Step 2: find the matching white reference

We import that white reference in the same way:

``` r

white_data <- lr_parse_oceanoptics_procspec(
  system.file("testdata", "procspec_files", "whiteref.ProcSpec",
               package = "lightr")
)
```

## Step 3: normalise the reflectance data

We can now normalise the reflectance spectrum with the equation stated
at the beginning of this vignette:

$`\text{Processed} = \frac{\text{Raw} - \text{Dark}}{\text{White} - \text{Dark}}`$

But first, we verify that the integration times:

We can now get rid of the metadata part and focus on the data only:

``` r

reflect_data <- data.frame(reflect_data[[1]])
white_data <- data.frame(white_data[[1]])
```

As a last step before being able to normalise the data, we also need to
check if the reflectance spectrum and the white reference are sampled
with the same wavelengths:

``` r

all.equal(reflect_data$wl, white_data$wl)
```

    ## [1] TRUE

``` r

res <- (reflect_data$scope - reflect_data$dark) / (white_data$white - white_data$dark)
head(res)
```

    ## [1]        NaN        NaN        NaN -5.3333333 46.0000000  0.6190476

Gruson, Hugo, Christine Andraud, Willy Daney de Marcillac, Serge
Berthier, Marianne Elias, and Doris Gomez. 2019. “Quantitative
Characterization of Iridescent Colours in Biological Studies: A Novel
Method Using Optical Theory.” *Interface Focus* 9 (1): 20180049.
<https://doi.org/10.1098/rsfs.2018.0049>.
