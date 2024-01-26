---
title: "solving captchas"
date: 2023-09-10T09:42:30+05:30
draft: false
tags: ['python']
---

\
solving captcha programatically is a pain. me and this other dude at work took about two weeks to solve version 2 of google recaptcha which we learned later, was an enterprise versioned captcha. i did not understand what that meant, until i read between the lines of the docs.

this blog is a simple sidenote on how to solve recaptcha (v2) with 2captcha API. you can read the [docs](https://2captcha.com/2captcha-api#solving_captchas), which btw, is amazing.

<center>
{{< figure src="/blog/recaptchav2.gif" width="250px" >}}
</center>

# prequisities

- 2captcha API key 
- install [requests](https://pypi.org/project/requests/)


{{% steps %}}

### step 1

right click around the captcha area --> inspect element

<center>
{{< figure src="/blog/inspectelement.png" width="350px" class="photoswipe" >}}
</center>

### step 2

find the "data-sitekey" parameter and copy the value. this will be the 'googlekey' value.

<center>
{{< figure src="/blog/sitekey_recaptcha.png" width="600px" class="photoswipe"  >}}
</center>

### step 3

send a http GET request to submit a captcha.


```python
import requests  #pip install requests

API_KEY = '1abc234de56fab7c89012d3'
URL = 'http://2captcha.com/in.php'
SITE = 'https://site-with-captcha.com'

response = requests.get(URL, 
    params = {
        'key': API_KEY, 
        'method': 'userrecaptcha', 
        'googlekey': 'key-from-step2',
        'pageurl' : SITE
    })
```

### step 4

if you came this far, you *will*  get the ID of your captcha as plain text, like:

```bash
OK|2122988149
```

if you get an error message, __do not proceed__ to the next step.
refer the [documentation](https://2captcha.com/2captcha-api#error_handling) if you get any errors.


### step 5

make a 15-20 seconds timeout and then, submit another GET request:       


```python
URL = 'http://2captcha.com/res.php'
response = requests.get(URL,
    params = {
        'key':API_KEY,
        'action': get,
        'id': 2122988149
    })
```


if captcha is already solved, server will respond with a randomly generated token. if it does not, you can repeat your request in 5 seconds.


### step 6

in developer's console, find the textarea with id="g-recaptcha-response", and send the received code. 


<center>
{{< figure src="/blog/g_recaptcha_response.png" width="600px" class="photoswipe" >}}
</center>


i used selenium to send the code back like so:

```python
driver.execute_script("""
    document.getElementById(
        "g-recaptcha-response"
        ).innerText='2122988149';
    """)
```

Then you can submit the captcha response, and recaptcha will be solved.


__Note:__  there is a high possibility these steps won't work. if you are looking for a direct method, you can find it [here](https://github.com/2captcha/2captcha-python/blob/master/examples/recaptcha_v2.py)



{{% /steps %}}