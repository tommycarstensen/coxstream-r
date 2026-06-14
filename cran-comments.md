# cran-comments

## Submission

New submission of coxstream 0.1.0.

## Test environments

- local: macOS (R 4.6.0), `R CMD check --as-cran`
- win-builder: devel and release, via `devtools::check_win_devel()` /
  `devtools::check_win_release()`
- R-hub / GitHub Actions: ubuntu-latest (release + devel), macOS, windows

## R CMD check results

0 errors | 0 warnings | 1 note

The single NOTE is the standard new-submission maintainer note:

* checking CRAN incoming feasibility ... NOTE
  Maintainer: 'Tommy Carstensen <cran@tommycarstensen.com>'
  New submission

The bundled header `src/arrow_c_abi.h` did not trigger a separate NOTE on the
local `--as-cran` run. For reviewer context: it is the ABI-stable Arrow C Data
Interface and C Stream Interface header, vendored verbatim from the Apache
Arrow project (Apache-2.0). It contains only plain-C struct layouts and
function-pointer signatures -- no Arrow source code -- and requires neither the
Arrow C++ headers nor linking against libarrow. This is acknowledged in
`inst/COPYRIGHTS` and in `Authors@R` (Apache Software Foundation, role cph).

## Reverse dependencies

None (new package).
