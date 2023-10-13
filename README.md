<!-- badges: start -->
[![Lifecycle: stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html#stable)
[![Project Status: Active - The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)
[![CRAN Version](https://www.r-pkg.org/badges/version/semptools?color=blue)](https://cran.r-project.org/package=semptools)
[![CRAN: Release Date](https://www.r-pkg.org/badges/last-release/semptools?color=blue)](https://cran.r-project.org/package=semptools)
[![CRAN RStudio mirror downloads](https://cranlogs.r-pkg.org/badges/grand-total/semptools?color=blue)](https://r-pkg.org/pkg/semptools)
[![Code size](https://img.shields.io/github/languages/code-size/sfcheung/semptools.svg)](https://github.com/sfcheung/semptools)
[![Last Commit at Master](https://img.shields.io/github/last-commit/sfcheung/semptools.svg)](https://github.com/sfcheung/semptools/commits/master)
[![R-CMD-check](https://github.com/sfcheung/semptools/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/sfcheung/semptools/actions/workflows/R-CMD-check.yaml)
<!-- badges: end -->

(Version 0.2.9.13, updated on 2023-10-13, [release history](https://sfcheung.github.io/semptools/news/index.html))

# semptools <img src="man/figures/logo.png" align="right" height="150" />

Helper functions for modifying (postprocessing) plots generated by `semPlot::semPaths()` from the `semPlot` package.

# Installation

The latest stable version can be installed from CRAN:

```r
install.packages("semptools")
```

The latest development version at GitHub can be installed by `remotes::install_github()`:

```r
remotes::install_github("sfcheung/semptools")
```

To read the guides (vignettes) on how to use the functions, you can build the vignettes locally when installing the package:

```r
remotes::install_github("sfcheung/semptools", build_vignettes = TRUE)
```

You can also find the guides under *Articles* of the [Github page](https://sfcheung.github.io/semptools/) of this package.

# Background

`semPlot::semPaths()` is a very useful function for visualizing structural equation models. We use it a lot. The output is a `qgraph` object which is highly customizable. Our area is in psychology and some users in this area may not know how to customize the graphs in aspects relevant to psychology. Therefore, we think it would be useful for users in psychology, including us, to have some functions for customizing the graphs from `semPlot::semPaths()`, without knowing the technical details of `qgraph`.

# Philosophy

We think about the tasks we usually want to do with an `semPlot::semPaths()` graph, and write one function for each task. We write the functions such that all of them work by postprocessing a `semPlot::semPaths()` graph: receive an `semPlot::semPaths()` graph, modify it, and return a modified `semPlot::semPaths()` graph. This also allows users to use the `%>%` (pipe) operator from the `magrittr` package or
the native pipe operator `|>` available since R 4.1.x to chain together modifications. For example:

```r
modified_graph <- original_graph %>%
                    task_1() %>%
                    task_2(other_arguments) %>%
                    task_3()
```

In psychology, two typical models are confirmatory factor analysis model and structural models with latent factors. Therefore, we also wrote two functions, one for each model, that can combine several common tasks together, such as specifying the positions of the latent factors and adjusting the positions of the indicators.

We also write the functions in a way that users do not need to know the technical detail (e.g., the position of the path in the list of all paths). For example, if a user wants to move the path coefficient of the path from `x` to `y` closer to `y`, the user only needs to tell the function that it is the path from `x` to `y`. The function will find which path it is in the `qgraph` object.

# What we have so far

These are some of the functions included so far

- `mark_se()`: Add the standard errors to parameter estimates.

- `mark_sig()`: Add asterisks ("\*", "\*\*", "\*\*\*") based on $p$-values of parameter estimates.

- `rotate_resid()`: Rotate the residuals of selected variables.

- `set_curve()`: Change the curvature of selected paths.

- `set_edge_label_position()`: Move the parameter labels of selected paths along the paths.

- `change_node_label()`: Change the labels of nodes.

- `drop_nodes()` and `keep_nodes()`: Drop or keeps nodes (e.g., drop all control variables).

- `set_cfa_layout()`: A function for typical confirmatory factor analysis models. It can be used for specifying the orders of the indicators and factors, specifying the positions of the factors, setting the curvatures of the interfactor covariances, set the position of all loadings, and setting the orientation of the model (down, left, up, or right).

- `set_sem_layout()`: A function for typical SEM models. It can be used for specifying the orders of the indicators and factors, specifying the positions of the factors using a grid, specifying the orientation of each factor's indicators (down, left, up, right), fine tuning the positions of indicators of selected factor, setting the curvatures of selected paths, and specifying the position of all or selected loadings.

See the [Get Started](https://sfcheung.github.io/semptools/articles/semptools.html) to learn more about these and other functions.

# Status

This package is still under development. There will be bugs, and there are limitations. Please
post your comments and suggestions as issues at [GitHub](https://github.com/sfcheung/semptools/issues).