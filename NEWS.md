# bignum (development version)

# bignum 0.3.0

* New `seq.bignum_vctr()` for generating sequences of `biginteger` or `bigfloat` (#30).

* To suppress lossy cast warnings, you should now use `suppressWarnings()` (#29).
    * If using R 4.1+, we recommend `suppressWarnings(expr, classes = "bignum_warning_cast_lossy")`.
    * Compatible with rlang 1.0.0.

* `vignette("operations")` has been removed and this documentation has been moved to man topics.

# bignum 0.2.2

* Adapted tests for testthat 3.1.0 (#27).

# bignum 0.2.1

* `format()` no longer checks for misspelled arguments. This previously caused issues when storing a bignum vector inside a data.frame or data.table (#25).

# bignum 0.2.0

## New features

* New `vignette("type-hierarchy")` and `vignette("precision")`.
* `format()` functions now support customized output.
    * New `sigfig` and `digits` arguments control the displayed precision.
    * New `notation` argument chooses decimal, scientific or hexadecimal output.
    * New options `"bignum.sigfig"` and `"bignum.max_dec_width"` determine the default formatting.
* When a bignum vector is stored in a [tibble](https://tibble.tidyverse.org) column, the formatting is adjusted to aid reading data vertically.
    * The decimal point and exponent are aligned across rows and negative numbers are colored red.
    * The options `"pillar.sigfig"` and `"pillar.max_dec_width"` determine tibble formatting.
    * See `vignette("digits", package = "pillar")` for details.
* `digamma()` and `trigamma()` operations are now supported.
* `log()` now supports the `base` argument.

## Bug fixes

* Casting a non-integer `double()` to `biginteger()` now returns the truncated integer, consistent with base vectors. Previously `NA` was returned. A lossy cast warning is still raised.
* Casting a large `double()` to `biginteger()` now works correctly. Previously `NA` was returned, depending on the value of `options("scipen")`.
* Casting `Inf` to `biginteger()` now raises a lossy cast warning.
* Casting a large `biginteger()` to `bigfloat()` now raises a lossy cast warning when the `bigfloat()` precision is exceeded.
* `is.finite()` and `is.infinite()` now correctly handle large `bigfloat()` values. Previously large values were considered infinite.
* Comparisons between `biginteger()` and `double()` vectors are now possible (e.g. `biginteger(2) > 1.5`). Previously a lossy cast error was raised.


# bignum 0.1.0

First CRAN release.

* Numeric vector classes:
    * `biginteger()` stores any integer (i.e. arbitrary precision).
    * `bigfloat()` stores 50 decimal digits of precision.

* Constants for common situations: `NA_biginteger_`, `NA_bigfloat_`, `bigpi`.

* Support for many basic operations (see `vignette("operations")`):
    * Check for special values: `is.na()`, `is.finite()`, `is.infinite()`,
      `is.nan()`
    * Comparison: `<`, `>`, `<=`, `>=`, `==`, `!=`
    * Arithmetic: `+`, `-`, `*`, `/`, `^`, `%%`, `%/%`
    * Mathematical:
        * `sum()`, `prod()`, `max()`, `min()`, `range()`, `mean()`
        * `cumsum()`, `cumprod()`, `cummax()`, `cummin()`
        * `floor()`, `ceiling()`, `trunc()`
        * `abs()`, `sign()`, `sqrt()`
        * `log()`, `log10()`, `log2()`, `log1p()`, `exp()`, `expm1()`
        * `cos()`, `sin()`, `tan()`, `acos()`, `asin()`, `atan()`, `cospi()`,
          `sinpi()`, `tanpi()`
        * `cosh()`, `sinh()`, `tanh()`, `acosh()`, `asinh()`, `atanh()`
        * `gamma()`, `lgamma()`, `factorial()`, `lfactorial()`
