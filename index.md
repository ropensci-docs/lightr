# `lightr`: import spectral data in R

There is no standard file format for spectrometry data and different
scientific instrumentation companies use wildly different formats to
store spectral data. Vendor proprietary software sometimes has an option
but convert those formats instead human readable files such as `csv` but
in the process, most metadata are lost. However, those metadata are
critical to ensure reproducibility ([White *et al*,
2015](https://doi.org/10.1016/j.anbehav.2015.05.007)).

This package aims at offering a unified user-friendly interface for
users to read UV-VIS reflectance/transmittance/absorbance spectra files
from various formats in a single line of code.

Additionally, it provides for the first time a fully free and open
source solution to read proprietary spectra file formats on all systems.

## 🗟 Citation

To cite this package in publications, please use:

> Gruson H., White T.E., Maia R., (2019). lightr: import spectral data
> and metadata in R. Journal of Open Source Software, 4(43), 1857,
> <https://doi.org/10.21105/joss.01857>

## 🔧 Installation

``` r

install.packages("lightr")
```

You can also install the development version from rOpenSci’s CRAN-like
repository:

``` r

install.packages("lightr", repos = "https://dev.ropensci.org")
```

## 💻 Usage

A thorough documentation is available with the package, using R usual
syntax `?function` or `help(function)`. However, users will probably
mainly use two functions:

``` r

# Get a data.frame containing all useful metadata from spectra in a folder
lr_get_metadata(where = system.file("testdata/procspec_files",
                                    package = "lightr"),
                ext = "ProcSpec")
```

and

``` r

# Get a single dataframe where the first column contains the wavelengths and
# the next columns contain a spectra each (pavo's rspec class)
lr_get_spec(where = system.file("testdata/procspec_files", package = "lightr"),
            ext = "ProcSpec")
```

[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
returns a dataframe that is compatible with
[`pavo`](https://cran.r-project.org/package=pavo) custom S3 class
(`rspec`) and can be used for further analyses using colour vision
models.

All supported file formats can also be parsed using the
`lr_parse_$extension()` function where `$extension` is the lowercase
extension of your file. This family of functions return a list where the
first element is the data dataframe and the second element is a vector
with relevant metadata.

Only exceptions are `.txt` and `.Transmission` files because those
extensions are too generic. Users will need to figure out which parser
is appropriate in this case.
[`lr_get_metadata()`](https://docs.ropensci.org/lightr/reference/lr_get_metadata.md)
and
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
automatically try generic parsers in this case.

Alternatively, you may simply want to convert your spectra in a readable
standard format and carry on with your analysis with another software.

In this case, you can run:

``` r

# Convert every single ProcSpec file to a csv file with the same name and
# location
lr_convert_tocsv(where = system.file("testdata/procspec_files",
                                      package = "lightr"),
                 ext = "ProcSpec")
```

## ✔ Supported file formats

This package is still under development but currently supports (you can
click on the extension in the tables to see an example of this file
format):

### [OceanOptics/OceanInsight](https://www.oceanoptics.com/)

| Extension | Parser |
|:---|:---|
| [`jdx`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/OceanOptics_period.jdx) | [`lr_parse_oceanoptics_jdx()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jdx.md) |
| [`ProcSpec`](https://github.com/ropensci/lightr/raw/main/inst/testdata/procspec_files/whiteref.ProcSpec) | [`lr_parse_oceanoptics_procspec()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_procspec.md) |
| [`spc`](https://github.com/ropensci/lightr/raw/main/inst/testdata/OceanOptics.spc) | [`lr_parse_oceanoptics_spc()`](https://docs.ropensci.org/lightr/reference/lr_parse_craic_spc.md) |
| [`jaz`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/jazspec.jaz) | [`lr_parse_oceanoptics_jaz()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jaz.md) |
| [`JazIrrad`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/irrad.JazIrrad) | [`lr_parse_oceanoptics_jazirrad()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jaz.md) |
| [`Transmission`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/FMNH6834.00000001.Master.Transmission) | [`lr_parse_oceanoptics_jaz()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jaz.md) |
| [`txt`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/OceanView.txt) | [`lr_parse_oceanoptics_jaz()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jaz.md) |

### [Avantes](https://www.avantes.com/)

| Extension | Parser |
|:---|:---|
| `ABS` | [`lr_parse_avantes_abs()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md) |
| [`ROH`](https://github.com/ropensci/lightr/raw/main/inst/testdata/avantes_reflect.ROH) | [`lr_parse_avantes_roh()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md) |
| [`TRM`](https://github.com/ropensci/lightr/raw/main/inst/testdata/avantes2.TRM) | [`lr_parse_avantes_trm()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md) |
| [`trt`](https://github.com/ropensci/lightr/raw/main/inst/testdata/avantes_export2.trt) | [`lr_parse_avantes_trt()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_ttt.md) |
| [`ttt`](https://github.com/ropensci/lightr/raw/main/inst/testdata/avantes_export.ttt) | [`lr_parse_avantes_ttt()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_ttt.md) |
| [`txt`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/avasoft8.txt) | [`lr_parse_generic()`](https://docs.ropensci.org/lightr/reference/lr_parse_generic.md) |
| [`DRK`](https://github.com/ropensci/lightr/raw/main/inst/testdata/1305084U1.DRK) | [`lr_parse_avantes_trm()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md) |
| [`REF`](https://github.com/ropensci/lightr/raw/main/inst/testdata/1305084U1.REF) | [`lr_parse_avantes_trm()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md) |
| [`IRR8`](https://github.com/ropensci/lightr/raw/main/inst/testdata/eg.IRR8) | [`lr_parse_avantes_irr8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md) |
| [`RFL8`](https://github.com/ropensci/lightr/raw/main/inst/testdata/compare/Avantes/feather.RFL8) | [`lr_parse_avantes_rfl8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md) |
| [`Raw8`](https://github.com/ropensci/lightr/raw/main/inst/testdata/1904090M1_0003.Raw8) | [`lr_parse_avantes_raw8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md) |

### [CRAIC](https://www.microspectra.com/)

| Extension | Parser |
|:---|:---|
| [`txt`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/CRAIC_export.txt) | [`lr_parse_generic()`](https://docs.ropensci.org/lightr/reference/lr_parse_generic.md) |
| [`spc`](https://github.com/ropensci/lightr/raw/main/inst/testdata/compare/CRAIC/CRAIC.spc) | [`lr_parse_craic_spc()`](https://docs.ropensci.org/lightr/reference/lr_parse_craic_spc.md) |

### [StellarNet](https://www.stellarnet.us/)

| Extension | Parser |
|:---|:---|
| `TRM` | [`lr_parse_generic()`](https://docs.ropensci.org/lightr/reference/lr_parse_generic.md) (\*) |

(\*) No automatic dispatch. Parser needs to be passed explicitly via the
`parser=` argument in
[`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md),
[`lr_get_metadata()`](https://docs.ropensci.org/lightr/reference/lr_get_metadata.md)
and
[`lr_convert_tocsv()`](https://docs.ropensci.org/lightr/reference/lr_convert_tocsv.md).

### Others

| Extension | Parser |
|:---|:---|
| [`csv`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/spec.csv) | [`lr_parse_csv()`](https://docs.ropensci.org/lightr/reference/lr_parse_csv.md) |
| [`dpt`](https://raw.githubusercontent.com/ropensci/lightr/main/inst/testdata/RS-1.dpt) | `lr_parse_generic(sep = ",")` |

As a fallback, you should always try
[`lr_parse_generic()`](https://docs.ropensci.org/lightr/reference/lr_parse_generic.md)
which offers a flexible and general algorithm that manages to extract
data from most files.

If you can’t find the best parser for your specific file or if you
believe you are using an unsupported format, please [open an
issue](https://github.com/ropensci/lightr/issues) or send me an email.

## 🌐 Similar projects

- `lightr` itself contains some code that has been initially forked from
  [`pavo`](https://cran.r-project.org/package=pavo), namely the
  [`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
  function. The code has since then been refactored and optimised for
  speed. [`pavo`](https://cran.r-project.org/package=pavo) differs from
  `lightr` in its focus and core functionalities. The main strength of
  [`pavo`](https://cran.r-project.org/package=pavo) is the comprehensive
  and user-friendly set of functions to analyse spectral data using
  [colour vision models](https://en.wikipedia.org/wiki/Color_model),
  while `lightr` focuses on the data import step.
- [`photobiologyInOut`](https://cran.r-project.org/package=photobiologyInOut)
  also provides functions to import spectral data. The goal of the
  author is to provide a complete pipeline of spectral data import and
  analysis using a [set of tightly integrated R
  packages](https://www.r4photobiology.info/). This however makes it
  more difficult to use a different tool for a given step of the
  process. On the contrary, `lightr` aims at proposing a light package
  with limited dependencies that focuses on the data import step of the
  process and let the user pick their favourite tool for the analysis
  step ([`pavo`](https://cran.r-project.org/package=pavo),
  [`colourvision`](https://cran.r-project.org/package=colourvision),
  [`Avicol`](https://sites.google.com/site/avicolprogram/), etc.).
- [`spectrolab`](https://github.com/meireles/spectrolab)

To our knowledge, `lightr` is the only gratis tool to import some
complex file formats such as Avantes (`ABS`, `ROH`, `TRM`, `RFL8`) or
CRAIC (`spc`) binary files, or OceanOptics `.ProcSpec`. Because of its
user-friendly high-levels functions and low dependency philosophy,
`lightr` may also hopefully prove useful for people working with other
languages than R.

## Contributing

There are plenty of ways you can contribute to `lightr`. Please visit
our [contributing
guide](https://docs.ropensci.org/lightr/CONTRIBUTING.html).

Please note that this package is released with a [Contributor Code of
Conduct](https://ropensci.org/code-of-conduct/). By contributing to this
project, you agree to abide by its terms.
