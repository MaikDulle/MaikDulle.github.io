---
layout: post
title: "LDA topic modeling of user generated content"
subtitle: "Using LDAvis to create topic models exploring users associations with online privacy"
background: '/img/posts/LDA-interactive/data-security.jpg'
---


LDA topic modeling using LDAvis
================

### Topic modeling of user’s privacy associations on Twitter and Instagram

As part of my dissertation, I examined user generated content (Posts &
Tweets) on the two Social media networks (SMNs) Twitter and Instagram.
More specifically I focussed on users’ privacy associations. I evaluated
the UGC with the help of two topic models (LDAvis package in R).

Here I present you the interactive results of the LDA models for Twitter
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

<iframe scr='/img/posts/LDA-interactive/Insta_LDA_model2.html' height="100%" width="100%"></iframe>

<br>

#### LDA topic model Twitter
