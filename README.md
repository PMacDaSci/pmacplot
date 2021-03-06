PMACPLOT
================

<!-- badges: start -->

[![R build
status](https://github.com/PMacDaSci/pmacplot/workflows/R-CMD-check/badge.svg)](https://github.com/PMacDaSci/pmacplot/actions/)
<!-- badges: end -->

This repo contains the functions of the `pmacplot` package, which once
installed locally, provides helpful functions for creating and exporting
graphics made in the style used by Peter Mac researchers (well that’s
the aim, it’s just beginning Nov 2020). It is based on the BBC news
bbplot package. This website also highlights plots researchers at Peter
Mac have created and shows the code for the plots.

# We need your help!

Would it be good if there was a uniform petermac ‘style’ that people
could use if they want?  
We could use the [bbc
style](https://github.com/bbc/bbplot/blob/master/R/bbc_style.R) as a
guide to discuss what aspects to use.  
Please let us know what you think and/or what plotting resources you
find useful [Google
doc](https://docs.google.com/document/d/1y3F0Xp91w3SCCALdUrqi8OswdMF8-Ek5_RrYK-9PDbI/edit)  
We would also love it if you have any example plots with code that we
could highlight here.

## Example plots

The figure below shows examples of plots created using the BBC news
package (that this package is based on). We’ll replace with examples
using this package when we have some. We’ve started adding some example
plots from Peter Mac researchers for inspiration. You can find them
under [Articles](https://pmacdasci.github.io/pmacplot/articles/) or in
the menu at the top of this page and reproduce them with the code shown.

![Example of graphics created using the pmacplot
package](man/figures/bbplot_example_plots.png)

## Installing pmacplot

`pmacplot` is not on CRAN, so you will have to install it directly from
Github using `remotes`.

If you do not have the `remotes` package installed, you will have to run
the first line in the code below as well.

``` r
# install.packages('remotes')
remotes::install_github('PMacDaSci/pmacplot')
```

## Using the functions

The package has two functions for plots: `petermac_style()` and
`finalise_plot()`.

Detailed examples on how to use the functions included within the
`pmacplot` package to produce graphics will be included at this website.
Examples for the BBC News versions can be found in the [R
cookbook](https://bbc.github.io/rcookbook/), as well as a more general
reference manual for working with `ggplot2`.

A basic explanation and summary here:

### `petermac_style()`

1.  `petermac_style()`: has no arguments and is added to the ggplot
    chain after you have created a plot. What it does is generally makes
    text size, font and colour, axis lines, axis text and many other
    standard chart components into Peter Mac style.

The function is pretty basic and does not change or adapt based on the
type of chart you are making, so in some cases you will need to make
additional `theme` arguments in your ggplot chain if you want to make
any additions or changes to the style, for example to add or remove
gridlines etc. Also note that colours for lines in the case of a line
chart or bars for a bar chart, do not come out of the box from the
`petermac_style` function, but need to be explicitly set in your other
standard `ggplot` chart functions.

Example of how it is used in a standard workflow:

``` r
line <- ggplot(line_df, aes(x = year, y = lifeExp)) +
geom_line(colour = "#007f7f", size = 1) +
geom_hline(yintercept = 0, size = 1, colour="#333333") +
petermac_style()
```

### `finalise_plot`

1.  `finalise_plot`: will save out your plot with the correct guidelines
    for publication for a Peter Mac graphic. It is made up of functions
    that will left align your title, subtitle and source and save it to
    your specified location. The function has six arguments, three of
    which need to be explicitly set and three that are defaults unless
    you overwrite them.

Here are the function arguments:
`finalise_plot(plot_name, source_name, save_filepath, width_pixels, height_pixels)`

-   `plot_name`: the variable name that you have called your plot, for
    example for the chart example above `plot_name` would be `"line"`  
-   `source_name`: the source text that you want to appear at the bottom
    left corner of your plot. You will need to type the word `"Source:"`
    before it, just the source, so for example `source = "Source: ONS"`
    would be the right way to do that.
-   `save_filepath`: the precise filepath that you want your graphic to
    save to, including the `.png` extension at the end. This does depend
    on your working directory and if you are in a specific R project. An
    example of a relative filepath would be: `/charts/line_chart.png`.  
-   `width_pixels`: this is set to 640px by default, so only call this
    argument and specify the width you want your chart to be.
-   `height_pixels`: this is set to 450px by default, so only call this
    argument and specify the height you want your chart to be.

Example of how the `finalise_plot()` is used in a standard workflow.
This function is called once you have created and finalised your chart
data, titles and added the `petermac_style()` to it (see above):

``` r
finalise_plot(plot_name = my_line_plot,
source = "Source: ONS",
save_filepath = "filename_that_my_plot_should_be_saved_to-nc.png",
width_pixels = 640,
height_pixels = 550)
```
