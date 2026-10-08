# cran-comments

## Submission

New submission of coxstream 0.1.0.

## Test environments

- local: macOS (R 4.6.0), `R CMD check --as-cran`
- win-builder: R-devel and R-release (source tarball uploaded)

## R CMD check results

0 errors | 0 warnings | 1 note

The single NOTE is the standard new-submission maintainer note. On
win-builder (R-devel) it additionally lists two "possibly misspelled words":

* checking CRAN incoming feasibility ... NOTE
  Maintainer: 'Tommy Carstensen <cran@tommycarstensen.com>'
  New submission
  Possibly misspelled words in DESCRIPTION:
    Efron (16:28)
    Raphson (3:16, 13:38)

Both flagged words are correctly spelled surnames: Bradley Efron (the Efron
tie-correction method) and the Newton-Raphson optimization algorithm. No
spelling change is warranted.

The bundled header `src/arrow_c_abi.h` did not trigger a separate NOTE on the
local `--as-cran` run. For reviewer context: it is the ABI-stable Arrow C Data
Interface and C Stream Interface header, vendored verbatim from the Apache
Arrow project (Apache-2.0). It contains only plain-C struct layouts and
function-pointer signatures -- no Arrow source code -- and requires neither the
Arrow C++ headers nor linking against libarrow. This is acknowledged in
`inst/COPYRIGHTS` and in `Authors@R` (Apache Software Foundation, role cph).

## Use of the Suggested `arrow` package

`coxstream_arrow()` uses only the exported `arrow` API. It allocates its own
`ArrowArrayStream` struct (whose ABI layout is the vendored `src/arrow_c_abi.h`
header) and fills it via the exported `RecordBatchReader$export_to_c()` method,
streaming parquet row groups into the package's C++ kernel through the
ABI-stable C struct contract. No unexported `arrow` function is called, and no
build-time dependency on the Arrow C++ libraries is required. `arrow` is a
Suggested (optional) dependency: the call is guarded with
`requireNamespace("arrow")` and errors with an install hint if absent, and the
core `coxstream()` fit does not use `arrow` at all.

## Reverse dependencies

None (new package).
