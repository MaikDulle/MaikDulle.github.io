---
layout: post
title: "Collecting Twitter tweets"
subtitle: "Using Twitter API to collect Starwars tweets"
background: '/img/posts/Twitter-API-collection/star-wars-g6aa903c6a_1920.jpg'
---

Collecting Twitter data using Twitter API
================

<br>

## Get your Twitter Developer Account

First, you have to set up a Twitter Developer Account. Go to
<https://developer.twitter.com/en/docs/twitter-api/getting-started/getting-access-to-the-twitter-api>
and sign up.

### Note: Use at your own risk. Be ethical about user data.

<br>

## Required libraries

``` r
library(rtweet)
library(dplyr)
library(ggplot2)
library(tidytext)
library(stringr)
```

<br>

## Create a Twitter App and generate necessary keys and tokens

In order to create an app, you need to log in to Twitter Developer
Account and click on "+add app".

![Create Twitter App](/img/posts/Twitter-API-collection/Create Twitter App.JPG)<!-- -->

<br>

Afterwards you need to generate the necessary keys/tokens to access the
official Twitter API (click on regenerate/yellow). 

![generate api key](/img/posts/Twitter-API-collection/generate api key.JPG)<!-- -->

<br>

![generate access token](/img/posts/Twitter-API-collection/generate access token.JPG)<!-- -->

<br>

I would advice to store those in your R script.
Note: These are fake example values. Please replace those with your own
keys.

``` r
api_key <- "yourownkey"
api_secret_key <- "xyz123456"
access_token <- "yourowntoken"
access_token_secret <- "xyz123456P"
```

<br>

## Authenticate via web browser

Note: The name of the app is an example, exchange for your own app name.

``` r
create_token(
  app = "Example_app",
  consumer_key = api_key,
  consumer_secret = api_secret_key,
  access_token = access_token,
  access_secret = access_token_secret)
```
<br>

## Start the madness

Here the collection process starts. We want to collect n= 500 tweets
including the hashtag #starwars

``` r
tweets_starwars <- search_tweets(q="#starwars",
                               n = 500)
```

<br>

## View the first 5 rows of the text in the dataframe

``` r
head(tweets_starwars$text, n = 5) 
```

<br>

## Count the most frequently used words

![starwars_tweets_word_count](/img/posts/Twitter-API-collection/starwars_tweets_word_count.png)<!-- -->
