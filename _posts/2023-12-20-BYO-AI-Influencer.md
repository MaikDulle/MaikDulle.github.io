---
layout: post
title: "Build your own AI-Influencer"
subtitle: "Using stable diffuson - A step by step guide"
background: '/img/posts/Website automation/gdpr-gcd4fb3122_1920.jpg'
---

## Note: Use at your own risk. Be ethical about usage. Further, I am not a professional programmer/developer.

## How to build your own AI-Influncer using stable difussion

I am using Automatic1111 because with some modification you can also use it with nearly every GPU (> 8 GB). For other stable diffusion UIs you often need NVIDIA GPU.

<br>

### Requirements before
First, make sure Python 3.10.6 is installed (https://www.python.org/downloads/release/python-3106/). IMPORTANT: Newer versions are not supported + In the installation process you need to click on 'Add Python to PATH'.
Second, you need to install GIT (https://git-scm.com/download/win).

<br>

### Download stable diffusion repo (and check for updates)
Create an empthy folder (e.g. called WEB UI) on your harddrive. Navigate to this emtpy folder to clone the repo to it. Then click in the upper path area and type 'cmd' Next you paste the following link and hit enter. The repo is then downloaded automatically.

``` r
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

![gifcmd](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

<br>

If you want to check for new updates (recom if something doesnt work anymore), you go into the 'stable-diffusion-webui' folder and 'git pull' into the cmd (same principle as the 'clone' command).

![pullcmd](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

<br>

### First start

Next you run the 'webui-user' from windows explorer by double clicking.

![webui](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

After the first start all dependencies etc. will be installed. This will take some time. Also a base model/checkpoint called 'v1-5-pruned-emaonly' will be downloaded. So you are basically set up to create your first images with stable diffusion.


<br>

### Configure webui-user.bat

In some cases (too little system resources), you can configurate the command line and tell the stable diffusion to use less resources. Here you will find all possible configuration options you can choose from: https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings#environment-variables

<br>

For weak GPUs maybe '--lowvram' is necessary. This increases the processing time a lot. In order to lower the Vram usage you can also try '--xformers'. For my system (16GB VRAM and Intel XE Iris onboard (i know pretty crap)), the following command line works perfectly fine. 

``` r
set COMMANDLINE_ARGS= --medvram --skip-torch-cuda-test --precision full --no-half
```

If you want to configure the commandline arguments, Right-click on the webui-user.bat and 'edit' it.

![configoptions](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

<br>

### General User Interface (GUI; local)

Here you can see the GUI of Automatic1111. I will just highlight the basic functions and options. The rest you can explore on your own ;)

<ul>
  <li>You can choose the model (green circle)</li>
  <li>The red circle marks where you can put in positive prompts (what you want) and negative prompts (what you want to avoid)</li>
  <li>You can choose the batch size (blue circle)</li>
  <li>You can choose the size of the image (yellow circle)</li>
  <li>You should set a seed if you want to recreate a similar picture (purple circle)</li>
  <li>You start image generation by clicking on 'Generate'</li>
</ul> 

![GUI_A1111](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

<br>

### Download other checkpoints

The base model downloaded when you first start stable diffusion is ok but you soon will want to go for better ones. You can find them online. One nice option is https://civitai.com/models. Here you can download different models/checkpoints for different purposes for free. You can just click on download. After downloading you have to add the checkpoint into the right folder (stable-diffusion-webui\models\Stable-diffusion)

![addcheckpoints](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

After putting the models into the right folder you can choose them after starting webui-user. (I downloaded the two checkpoint 'Juggernaut' and 'Newreality')

![modelchoice](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

<br>

### Prompting (pos/neg)

Positive prompts are the things you want in an image (e.g. blue eyes)
Negative prompts are thins you want to avoid in an image (e.g. oversaturated or ugly)

The cool thing about civitai is that if you click on a picture of a checkpoint (e.g. https://civitai.com/images/3962887) the used settings are shown. So you can copy and paste the negative prompts to improve your generation easily. And reading through different pos. prompts will help you to improve your own prompting.

![modelchoice](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

<br>

### First try on my own

For my first try I wanted to create a male business influencer. Here is what I tried.

<ul>
  <li>Positive prompt: Business man, handsome, office, portrait, brown hair, blue eyes, down-to-earth, elegant, sharp focus, soft lighting, vibrant colors, hyperdetailed photography</li>
  <li>Negative prompt: disfigured, ugly, oversaturated, low quality, bad eyes</li>
  <li>Seed: random (-1)</li>
</ul> 

And here is the result. Except for a little bit of weirdness in the eye region I would say quite impressive.

![example1](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

### Troubleshooting and some more examples

Also in the repo you can finde some more advice about troubleshooting. Check you this info:
https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Troubleshooting

<br>

And here are 2 more examples I created:

![example2](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

![example3](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

![example3](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

Happy prompting and generating! :)

<br>

This project is inspired by https://www.youtube.com/watch?v=ky5ZB-mqZKM.
