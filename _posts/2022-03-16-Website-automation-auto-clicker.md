---
layout: post
title: "Simple website automation"
subtitle: "Website automation in TOR browser"
background: '/img/posts/Website automation/gdpr-gcd4fb3122_1920.jpg'
---

## Note: Use at your own risk. Be ethical about usage. Further, I am not a professional programmer/developer.

This little examples only shows how easy you can automate navigation and clicks on websites. While the code of example I is running, you can not use the computer because it would interfere with pyautogui. Example II is fully automated. I used Jupyter Notebook to run the code.

![spongebob_gif_automation](/img/posts/Website automation/spongebob_gif_automation.gif)<!-- -->

<br>

### Simple example I
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
<br>

### Still simple but a little more sophisticated example II

### Requirements
``` r
import requests
from stem import Signal
from stem.control import Controller
import random
import time
```
<br>

### Define parameters
``` r
# Set the URL and headers for the request
url = 'https://website_you_want_to_visit'
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36"
}
```

<br>

### Automation function
``` r
# Set the number of requests to send (modify if need be)
num_requests = 5

# Establish a connection to the Tor control port
with Controller.from_port(port=9051) as controller:
    # Authenticate to the control port
    controller.authenticate()

    for _ in range(num_requests):
        try:
            # Request a new circuit
            controller.signal(Signal.NEWNYM)

            # Generate a random delay between 5 and 90 seconds (modify if need be)
            delay = random.randint(5, 90)
            time.sleep(delay)

            # Set the proxy for the requests library
            session = requests.session()
            session.proxies = {'http': 'socks5://localhost:9150',
                               'https': 'socks5://localhost:9150'}

            # Send the request
            response = session.get(url, headers=headers)

            # Print the response
            print("IP address: %s" % session.get("http://httpbin.org/ip").text.strip()) # check the used IP and if it really rotates
            #print(response.text)
        except Exception as e:
            print(f"An error occurred: {str(e)}")
```

<br>

