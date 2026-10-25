# Package index

## High-level functions

These functions offers an intuitive and user-friendly way to import (and
possibly) transform multiple files at once in a given location. Please
refer to the [*Batch import with `lr_get_spec()` and
`lr_get_metadata()`*
vignette](https://docs.ropensci.org/lightr/articles/batch_import.md).

- [`lr_get_spec()`](https://docs.ropensci.org/lightr/reference/lr_get_spec.md)
  : Extract spectral data from spectra files
- [`lr_get_metadata()`](https://docs.ropensci.org/lightr/reference/lr_get_metadata.md)
  : Extract metadata from spectra files
- [`lr_convert_tocsv()`](https://docs.ropensci.org/lightr/reference/lr_convert_tocsv.md)
  : Convert spectral data files to csv files

## Low-level parsers

These functions are destined to advanced users that want a more flexible
way to import spectral data. They can only read a single file at a time
and users are responsible for writing a loop if necessary. . Please
refer to the [*Renormalise spectral data with a custom reference*
vignette](https://docs.ropensci.org/lightr/articles/batch_import.md).

- [`lr_parse_trm()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_abs()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_roh()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_rfl8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_raw8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_irr8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_avantes_trm()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_avantes_abs()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_avantes_roh()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_avantes_rfl8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_avantes_raw8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  [`lr_parse_avantes_irr8()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_trm.md)
  : Parse Avantes binary file
- [`lr_parse_ttt()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_ttt.md)
  [`lr_parse_trt()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_ttt.md)
  [`lr_parse_avantes_ttt()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_ttt.md)
  [`lr_parse_avantes_trt()`](https://docs.ropensci.org/lightr/reference/lr_parse_avantes_ttt.md)
  : Parse Avantes converted file
- [`lr_parse_spc()`](https://docs.ropensci.org/lightr/reference/lr_parse_craic_spc.md)
  [`lr_parse_craic_spc()`](https://docs.ropensci.org/lightr/reference/lr_parse_craic_spc.md)
  [`lr_parse_oceanoptics_spc()`](https://docs.ropensci.org/lightr/reference/lr_parse_craic_spc.md)
  : Parse SPC binary file
- [`lr_parse_csv()`](https://docs.ropensci.org/lightr/reference/lr_parse_csv.md)
  : Parse csv files
- [`lr_parse_generic()`](https://docs.ropensci.org/lightr/reference/lr_parse_generic.md)
  : Generic function to parse spectra files that don't have a specific
  parser
- [`lr_parse_jaz()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jaz.md)
  [`lr_parse_jazirrad()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jaz.md)
  [`lr_parse_oceanoptics_jaz()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jaz.md)
  [`lr_parse_oceanoptics_jazirrad()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jaz.md)
  : Parse OceanOptics converted file
- [`lr_parse_jdx()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jdx.md)
  [`lr_parse_oceanoptics_jdx()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_jdx.md)
  : Parse OceanOptics JCAMP-DX (.jdx) file
- [`lr_parse_procspec()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_procspec.md)
  [`lr_parse_oceanoptics_procspec()`](https://docs.ropensci.org/lightr/reference/lr_parse_oceanoptics_procspec.md)
  : Parse OceanOptics ProcSpec file

## Internal functions

- [`dispatch_parser()`](https://docs.ropensci.org/lightr/reference/dispatch_parser.md)
  : Internal function to dispatch files to the correct parser
- [`lightr`](https://docs.ropensci.org/lightr/reference/lightr-package.md)
  [`lightr-package`](https://docs.ropensci.org/lightr/reference/lightr-package.md)
  : lightr: Read Spectrometric Data and Metadata
- [`lr_compute_processed()`](https://docs.ropensci.org/lightr/reference/lr_compute_processed.md)
  : Compute processed spectral data
