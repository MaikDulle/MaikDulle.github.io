---
layout: post
title: "How to extract frames from videos"
subtitle: "Works for single and multiple videos"
background: '/img/posts/extract_frames/coding-924920_1280.jpg'
---

## Note: Use at your own risk. Be ethical about usage. Further, I am not a professional programmer/developer.
<br>
## How to extract frames from (multiple) videos

This little Code Snippet allows you to extract frames from one or multiple videos. 

<br>

### Requirements
``` r
import os
import numpy as np
import cv2
from glob import glob
```
<br>

### Change directory
``` r
os.chdir('d:\\your\\path') 
```

<br>

### Create directory
``` r
def create_dir(path):
    try:
        if not os.path.exists(path):
            os.makedirs(path)
    except OSError:
        print(f"ERROR: creating dir with name {path}")
```

<br>

### Extract frames from video 

To do so we use the CV2 package
``` r
def save_frame(video_path, save_dir, gap=100): #specify the gap
    name = video_path.split("/")[-1].split(".")[0]
    save_path = os.path.join(save_dir, name)
    create_dir(save_path)

    cap = cv2.VideoCapture(video_path)
    idx = 0 # this is the zero frame

    while True:
        ret, frame = cap.read()

        if ret == False:
            cap.release()
            break

        if idx == 0:
            cv2.imwrite(f"{save_path}/{idx}.png", frame)
        else:
            if idx % gap == 0:
                cv2.imwrite(f"{save_path}/{idx}.png", frame)

        idx += 1

if __name__ == "__main__":
    video_paths = glob("videos/*")
    save_dir = "save"

    for path in video_paths:
        save_frame(path, save_dir, gap=100) #specify the gap
```  

Now just put the videos you want to extract frames from in the video folder. Make sure the directory is set correctly and run the script. The output you will find in the save folder.

<br>

Here is a demo gif. Hope this will work for you too and happy coding :)

![working_example_frames](/img/posts/extract_frames/working_example_frames.gif)<!-- -->

This project is inspired by https://github.com/nikhilroxtomar.
