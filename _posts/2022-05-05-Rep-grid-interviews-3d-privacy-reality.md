---
layout: post
title: "3d visualization of privacy perception"
subtitle: "3d visualization of repertory-grid-interviews"
background: '/img/posts/3dslater-privacy-personalization/1 1e6J5KYYvwlOXRVj9-RkQA.png'
---

Repertory Grid Interviews with regard to personalization and privacy protection
================

As part of my dissertation, I interviewed users via repertory-grid-interview. Specifically, I asked users about their attitude towards personalization and privacy protection
I eanalyzed the interviews using the OpenRepGrid package in R and created a 3d model (Slater biplot) of user privacy reality/perception across all 16 participants.

For detailed infos check the vignette of OpenRepGrid:
<https://cran.r-project.org/web/packages/OpenRepGrid/OpenRepGrid.pdf>

After ploting, a html-doc was created via html:widget in order to embed the models in this post.

Here I am solely presenting the interactive 3d Slater biplot (Interpretation can be found in my dissertation)

Note: Be ethical about user data.


### required libraries

``` r
library(OpenRepGrid)
library(rgl)
library(htmlwidgets)
```

<br>

### load grids

Grids you want to import follow the format:

1 | E1 | E2 | E3 | E4 | 5
-- | -- | -- | -- | -- | --
left pole | 1 | 5 | 3 | 4 | right pole 
left pole | 3 | 1 | 1 | 3 | right pole
left pole | 4 | 2 | 5 | 1 | right pole

``` r
# load different grid interviews
# this is just example code
Grid1 <- importExcel("your path+document name.xlsx", min = 1, max = 5) # define min and max value of grid
Grid2 <- importExcel("your path+document name.xlsx", min = 1, max = 5)
Grid3 <- importExcel("your path+document name.xlsx", min = 1, max = 5)
```

<br>

### combine grids to one long grid

``` r
# this is just example code
Gridall <- bindConstructs(Grid1, Grid2, Grid3)
```

<br>

### plot 3d Slater biplot

<iframe id = '3d_slater_privacy' src="/img/posts/3dslater-privacy-personalization/Grid_3d_viz.html"
    sandbox="allow-same-origin allow-scripts"
    width="1210"
    height="800"
    scrolling='no'
    seamless
    frameborder="0">
</iframe>

### saving options (pdf, png, ...)
``` r
#save 3d plot as pdf
rgl.postscript("biplot3d.pdf", "pdf")

#take a png screenshot
rgl.snapshot("your path+document name.png", fmt = "png")

# save as a standalone html-doc
htmlwidgets::saveWidget(rglwidget(width = '800', height = '600'), "your path+document name.html")
```