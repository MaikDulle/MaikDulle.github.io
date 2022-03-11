---
layout: post
title: "LDA topic modeling with LDAvis"
subtitle: "Topic modeling of user generated content with regard to online privacy associations"
background: '/img/posts/LDA-interactive/data-security.jpg'
---

LDA topic modeling using LDAvis
================

### Topic modeling of user’s privacy associations on Twitter and Instagram

As part of my dissertation, I examined user generated content (UGC = Posts &
Tweets) on Twitter and Instagram.
More specifically I focussed on users’ privacy associations. I evaluated
the UGC with help of two topic models (LDAvis package in R).

A very helpful description of the modeling process can be found here: https://ldavis.cpsievert.me/reviews/reviews.html

After modeling, html-docs were created via pyLDAvis in order to embed the models in this post.

Here I am solely presenting the interactive results of the LDA models for Instagram
and Twitter. (Interpretation can be found in my dissertation)

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


<div style="text-align:center">
    <iframe id = 'lda_insta' src="/img/posts/LDA-interactive/Insta_LDA_model2.html"
        sandbox="allow-same-origin allow-scripts"
        width="1210"
        height="800"
        scrolling='no'
        seamless
        frameborder="0">
    </iframe>
 </div>



<br>

#### LDA topic model Twitter

<div style="text-align:center">
    <iframe id = 'lda_twitter' src="/img/posts/LDA-interactive/Twitter_LDA_model2.html"
        sandbox="allow-same-origin allow-scripts"
        width="1210"
        height="800"
        scrolling='no'
        seamless
        frameborder="0">
    </iframe>
 </div>