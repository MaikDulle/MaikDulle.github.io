---
layout: post
title: "Simple website automation"
subtitle: "Website automation in TOR browser"
background: '/img/posts/Website automation/gdpr-gcd4fb3122_1920.jpg'
---

## Note: Use at your own risk. Be ethical about usage. Further, I am not a professional programmer/developer.

This little code only shows how easy you can automate navigation and clicks on website. While the code is running you can not use the computer because it would interfere with pyautogui. I used Jupyter Notebook to run the code.

![spongebob_gif_automation](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

<br>

### Requirements
``` r
import webbrowser
import time
import pyautogui
```
<br>

### Define parameters
``` r
url = 'https://website_you_want_to_visit'
count = 0
max_guesses_allowed = 20
```

<br>

### Automation function
``` r
def repeat():
    tor_path = \
        'C:\\Path\\of\\Tor Browser\\firefox.exe'
    webbrowser.register('tor', None, webbrowser.BackgroundBrowser(tor_path))
    webbrowser.get('tor').open(url)
    time.sleep(70) # give browser time to open cookie
    pyautogui.moveTo(743,627,3) # position to accept cookie by clicking on "accept"
    time.sleep(15)
    pyautogui.click()
    time.sleep(100) # time on page
    pyautogui.moveTo(1073,54,3) # position to close webbrowser by clicking X
    time.sleep(15)
    pyautogui.click()
    time.sleep(20)
```

<br>

### Loop the automation function    
``` r
while True or count < max_guesses_allowed:
   repeat()
   count += 1
```  

<br>

### Detect position on screen

Use this line to detect on which position on the screen the obejcts are you want to click on (Cookie-accept-button or Closing-brwoser-X)

``` r
print(pyautogui.position())
```
