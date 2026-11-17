---
layout: post
title: "AI Project: The Trade Counsil"
subtitle: "Analyst, Trader, Risk Officer: what an AI stock desk taught me about making decisions"
author: Dr. Maik Dulle
date: 2026-11-17
background: '/img/posts/thetradecounsil/tbd.png'
---

#### Note: All numeric values in this example are ficticious and serve for the purpose of illustration only. Use at your own risk. Be ethical about usage. Further, I am not a professional programmer/developer.

---

# Three opinions before one trade

As a data analyst, I work with data every day, and most of that work and insights result in a decision somebody has to make. Over the last few weeks I built a side project that applies the same habits to a more personal question: should I buy this stock?

It's called Trade Council. You give it a stock idea and three AI perspectives look at and evaluate it. An analyst checks the numbers. A trader checks the timing. A risk officer asks what could go wrong and what it would cost you. They often disagree, and the app shows the disagreement instead of hiding it in an average.

![Trade Council](images/cover.png)

The part I find interesting is the decision process. A few habits from data science fit it better than I expected.

## Write the plan before you see the result

In an A/B test you fix the success metric before the test runs. If you don't, you'll find some metric that makes your favourite variant win. The app does the same thing around earnings reports: you decide beforehand which numbers would make you buy. After the report you only tick boxes.

## Decide how much you can lose first

Every plan starts with the stop, the price at which you admit you were wrong, and the loss in euros if it gets hit. The amount you invest is calculated from that. The sidebar shows how a trade fits into the budget you set yourself, and the loss limit per trade scales with that budget.

![The money sidebar](images/your-money.png)

## A "wait" needs a plan too

Most models I build end in a score or an estimate. Those are quite easy to interpret, the hard part is what people do with a "not yet". Here every "wait" comes with a watch card: which price alerts to set, when to look again, and what has to happen before buying. You check it on a few fixed dates and leave the chart alone in between (no cherry-picking).

![A watch card, in German and dark mode](images/watch-card-de-dark.png)

## Judge the process, not only the outcome

A good decision can lose money and a bad one can win. The journal records how confident each call was and how it turned out. After a while you can see whether the "high confidence" calls really do better than the medium ones. That's a calibration check, the same one I'd run on any classifier.

## What it is

It's a learning project. The analysis comes from an AI model, it can be wrong, and it isn't financial advice. I mostly use it to slow down and to see the reasoning written out before I click buy.

The code is free on GitHub: one HTML file that runs in your browser with your own Claude API key, plus a Claude skill.

[github.com//MaikDulle/Trade_Counsil](https://github.com//MaikDulle/Trade_Counsil)

Thats a wrap for this post. Try it yourself and happy experimenting! :)