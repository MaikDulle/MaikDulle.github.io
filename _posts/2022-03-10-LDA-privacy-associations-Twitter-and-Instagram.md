---
layout: post
title: "LDA topic modeling with LDAvis"
subtitle: "Topic modeling of user generated content with regard to online privacy associations"
background: '/img/posts/LDA-interactive/data-security.jpg'
---

LDA topic modeling using LDAvis
================

### Topic modeling of user’s privacy associations on Twitter and Instagram

As part of my dissertation, I examined user generated content (Posts &
Tweets) on the two Social media networks (SMNs) Twitter and Instagram.
More specifically I focussed on users’ privacy associations. I evaluated
the UGC with the help of two topic models (LDAvis package in R).

A more detailed description of the procedure: https://ldavis.cpsievert.me/reviews/reviews.html

Here I present the interactive results of the LDA models for Twitter
and Instagram.

Note: Be ethical about user data.

<br>

#### Requirements

``` r
library(lda)
library(LDAvis)
library(tm)
library(dplyr)
library(textclean)
library(stringr)
library(jsonlite)
library(rjson)
```

<br>

#### LDA topic model Instagram

<p align="center">
    <iframe id = 'lda_insta' src="/img/posts/LDA-interactive/Insta_LDA_model2.html"
        sandbox="allow-same-origin allow-scripts"
        width="1210"
        height="800"
        scrolling='no'
        seamless
        frameborder="0"
        style="text-align: center"
        >
    </iframe>
 </p>


<br>

#### LDA topic model Twitter
