# iea-ak-info

Integrated Ecosystem Assessment - Alaska - infographics

This website is an initial demonstration of using a simple interactive infographics implementation based on JavaScript only (ie not using the R-based [infographiq](https://github.com/marinebon/infographiq)).

## technical implementation

The illustration in scalable vector graphics (`.svg`) format has individual elements given an identefier (ie `id`) which are linked to popup (ie "modal") windows of content using a simple table in comma-seperated value (`.csv`) format using [d3](https://d3js.org).

### core files: `.svg`, `.csv`

In this example for the Eastern Bering Sea (`ebs`), these two files are at the core of the infographic construction:

1. **illustration**: [`ebs.svg`](https://github.com/marinebon/iea-ak-info/blob/master/svg/ebs.svg) 
1. **table**: [`ebs_links.csv`](https://github.com/marinebon/iea-ak-info/blob/master/svg/ebs_links.csv) 

Each `link` in the table per element identified (`id`) is the page of content displayed in the modal popup window when the given element is clicked. The `title` determines the name on hover and title of the modal window.

### html and js/css dependencies

The illustration (`.svg`) and table (`.csv`) get rendered with the `link_svg()` function (defined in `infographiq.js`) with the following HTML:

```html
<!-- load dependencies on JS & CSS -->
<script src='https://d3js.org/d3.v5.min.js'></script>
<script src='infographiq.js'></script>

<!-- add placeholder in page for placement of svg -->
<div id='svg'></div>

<!-- run function to link the svg -->
<script>link_svg(svg='svg/ebs.svg', csv='svg/ebs_links.csv');</script>
```

The modal popup windows are rendered by [Bootstrap modals](https://getbootstrap.com/docs/3.3/javascript/#modals). This dependency is included with the default Rmarkdown rendering, but if you need to seperately include it then add this HTML:

```html
<!-- load dependencies on JS & CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
```

## build and view website in R

This website is constructed using [Rmarkdown website](https://bookdown.org/yihui/rmarkdown/rmarkdown-site.html) for enabling easy construction of site-wide navigation (see [`_site.yml`](https://github.com/marinebon/iea-ak-info/blob/master/_site.yml)) and embedding of [htmlwidgets](https://www.htmlwidgets.org), which provide interactive maps, time series plots, etc into the html pages to populate the modal window content in [`modals/`](https://github.com/marinebon/iea-ak-info/tree/master/modals). To build the website and view it, here are the commands to run in R:

```r
# build website
source("render_site.R")

# serve website
servr::httd("docs")
```

The [`render_site.R`](https://github.com/marinebon/iea-ak-info/blob/master/render_site.R) script renders the modal and website pages.

Note the actual html content served at [marinebon.github.io/iea-ak-info](https://marinebon.github.io/iea-ak-info) via [Github Pages](https://pages.github.com/) is all the html/jss/csss files copied into the `docs/` folder of this repository.

