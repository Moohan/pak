
<!-- README.md is generated from README.Rmd. Please edit that file -->

# pak

> A Fresh Approach to R Package Installation

<!-- badges: start -->

![lifecycle](https://img.shields.io/badge/lifecycle-experimental-orange.svg)
[![](https://www.r-pkg.org/badges/version/pak)](https://cran.r-project.org/package=pak)
[![CRAN RStudio mirror
downloads](https://cranlogs.r-pkg.org/badges/pak)](https://www.r-pkg.org/pkg/pak)
[![Codecov test
coverage](https://codecov.io/gh/r-lib/pak/branch/main/graph/badge.svg)](https://app.codecov.io/gh/r-lib/pak?branch=main)
[![R-CMD-check](https://github.com/r-lib/pak/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/r-lib/pak/actions/workflows/R-CMD-check.yaml)

<!-- badges: end -->

pak installs R packages from CRAN, Bioconductor, GitHub, URLs, local
files and directories. It is an alternative to `install.packages()` and
`devtools::install_github()`. pak is fast, safe and convenient.

<p align="center">
<img width="1000" src="https://cdn.jsdelivr.net/gh/r-lib/pak@images/pak-demo.svg?version=2">
</p>

## Installation

### Pre-built binaries

Install a binary build of pak from our repository on GitHub:

``` r
install.packages("pak", repos = sprintf("https://r-lib.github.io/p/pak/stable/%s/%s/%s", .Platform$pkgType, R.Version()$os, R.Version()$arch))
```

This is supported for the following systems:

| OS                 | CPU     | R version         |
|--------------------|---------|-------------------|
| Linux              | x86_64  | R 3.4.0 - R-devel |
| Linux              | aarch64 | R 3.4.0 - R-devel |
| macOS High Sierra+ | x86_64  | R 3.4.0 - R-devel |
| macOS Big Sur+     | aarch64 | R 4.1.0 - R-devel |
| Windows            | x86_64  | R 3.4.0 - R-devel |

For macOS we only support the official CRAN R build. Other builds, e.g.
Homebrew R, are not supported.

### Install from CRAN

Install the released version of the package from CRAN as usual:

``` r
install.packages("pak")
```

This potentially needs a C compiler on platforms CRAN does not have
binaries packages for.

### Nightly builds

We have nightly binary builds, for the same systems as the table above:

``` r
install.packages("pak", repos = sprintf("https://r-lib.github.io/p/pak/devel/%s/%s/%s", .Platform$pkgType, R.Version()$os, R.Version()$arch))
```

### `stable`, `rc` and `devel` streams

We have three types of binaries available: \* `stable` corresponds to
the latest CRAN release of CRAN. \* `rc` is a release candidate build,
and it is available about 1-2 weeks before a release. Otherwise it is
the same as the `stable` build. \* `devel` has builds from the
development tree. Before release it might be the same as the `rc` build.

The streams are available under different repository URLs:

``` r
stream <- "rc"
install.packages("pak", repos = sprintf("https://r-lib.github.io/p/pak/%s/%s/%s/%s", stream, .Platform$pkgType, R.Version()$os, R.Version()$arch))
```

## Usage

Call `pkg_install()` to install CRAN or Bioconductor packages:

``` r
pak::pkg_install("usethis")
```

To install packages from GitHub, use the `user/repo` syntax:

``` r
pak::pkg_install("r-lib/usethis")
```

All dependencies will be installed as well, to the same library.

### On GitHub Actions

The
[`setup-r-dependencies`](https://github.com/r-lib/actions/tree/v2/setup-r-dependencies#setup-r-dependencies)
action at [`r-lib/actions`](https://github.com/r-lib/actions) uses pak
to install packages. See the
[`examples`](https://github.com/r-lib/actions/tree/v2/examples)
directory for example workflows.

## Why pak?

### Fast

-   Fast downloads and HTTP queries. pak performs all HTTP requests
    concurrently.

-   Fast installs. pak builds and installs packages concurrently.

-   Metadata and package cache. pak caches package metadata and all
    downloaded packages locally. It does not download the same package
    files over and over again.

-   Lazy installation. pak only installs the packages that are really
    necessary for the installation. If the requested package and its
    dependencies are already installed, pak does nothing.

### Safe

-   Private library (pak’s own package dependencies do not affect your
    regular package libraries and vice versa).

-   Every pak operation runs in a sub-process, and the packages are
    loaded from the private library. pak avoids loading packages from
    your regular package libraries. (These package files would be locked
    on some systems, and locked packages cannot be updated. pak does not
    load any package in the main process, except for pak itself).

-   To avoid updating locked packages, pak offers the choice of
    unloading them from the current R session, and/or killing other R
    sessions locking them.

-   Dependency solver. pak makes sure that you end up in a consistent,
    working state of dependencies. It finds conflicts up front, before
    attempting installation.

-   System package support. pak automatically installs system
    dependencies on several Linux distributions.

### Convenient

-   BioC packages. pak supports Bioconductor packages out of the box. It
    uses the Bioconductor version that is appropriate for your R
    version.

-   GitHub packages. pak supports GitHub packages out of the box. It
    also supports the `Remotes` entry in `DESCRIPTION` files, so that
    GitHub dependencies of GitHub packages will also get installed. See
    e.g.
    <https://cran.r-project.org/package=remotes/vignettes/dependencies.html>

-   Easy time travel with [MRAN](https://mran.microsoft.com/timemachine)
    and [RSPM](https://packagemanager.rstudio.com/client/#/), to a
    specific date or when a certain R or package version was released.

-   Package sizes. For CRAN packages pak shows the total sizes of
    packages it needs to download.

-   Other package sources:

    -   local package files and directories,
    -   URLs to package files or package tree archives.

## Roadmap

-   Cache locally installed packages.
-   Update installed packages.
-   Better integration with renv.
-   Support more package sources: Enterprise GitHub, GitLab, Bitbucket
    and SVN repositories.
-   Support older CRAN and Bioconductor packages.
-   More comprehensive system requirements support.

## License

GPL-3 © RStudio
