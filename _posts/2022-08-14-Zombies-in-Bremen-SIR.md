---
layout: post
title: "Zombies in Bremen"
subtitle: "Modeling a zombie outbreak in the city of Bremen, Germany"
background: '/img/posts/zombies-in-bremen/5990108.jpg'
---

## Zombies in Bremen

I modeled a zombie outbreak in the city of Bremen in Germany. The
outbreak follows a classic SIR model. SIR models are used to describe
disease transmission (or in our case transforming from human to zombie)
within a population. The letters stand for:

-   S = the number of SUSCEPTIBLE individuals/healthy, still
    non-infected individuals
-   I = the number of INFECTED individuals/number of zombies
-   R = if you model the flu, R would stand for RECOVERED individuals.
    Since you normally can’t recover from turining into a zombie, R
    stands for REMOVED zombies and describes the number of zombies
    eliminanted by non-infected individuals

Further, the model included the two parameters beta and gamma. Beta
describes the infection rate (how quickly the infection is spreading)
and gamma describes zombie death/elimination rate. For the next model I
used a beta of 0.3 and a gamma of 0.05 (since not everybody is a natural
born zombie hunter)

I placed the patient zero in the city center of Bremen because a crowded
place is most likely the starting point of the apocalypse.

Note. I didnt not come up with the model specification myself, but was
rather inspired by a cool project you can find here:
<http://maxberggren.se/2014/11/27/model-of-a-zombie-outbreak/>

## Spread model

<style>
  /* Container to control the size of the iframe */
  .iframe-container {
    position: relative;
    overflow: hidden;
    /* Set the aspect ratio (width:height) of your iframe */
    padding-top: 56.25%; /* 16:9 aspect ratio (9 / 16 * 100) */
  }

  /* Make the iframe fill the container */
  .responsive-iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
</style>

<body>

  <!-- Container div for the iframe -->
  <div class="iframe-container">
      <!-- Your iframe goes here -->
    <iframe 
      class="responsive-iframe"
      id = 'SIR-zombies' 
      src="/img/posts/zombies-in-bremen/Bremen_outbreak.gif" 
      frameborder="0" allowfullscreen>
    </iframe>
  </div>
</body>


The city center would quickly turn into a zombie stronghold and would no longer be safe.

<br>

## Visualize the development

![](/img/posts/zombies-in-bremen/SIR model zombies in Bremen.png)<!-- -->

In this visualization I set the total population to 569.352 (number of
citizens in Bremen 2019). Beta and gamma stayed the same. As we can see after 40 days there is little
hope left and the zombies take over entirely. Of course the scenario is
rather pessimistic, but otherwise it would only be half as interesting.
