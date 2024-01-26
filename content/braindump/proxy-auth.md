---
title: "setting up proxies in selenium"
date: 2023-09-11T20:32:32+05:30
draft: false
tags: ['selenium', 'python']
---

this is a sample configuration of using proxies with IP authentication, using selenium and python.


### sample code

 ```python
CHROMEDRIVER_PATH = /path/to/chromedriver
PROXY = "23.23.23.23:3128" # IP:PORT 
URL = 'https://example.com'

from seleniumwire import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.chrome.service import Service

options = Options()
options.add_argument('--proxy-server=%s' % PROXY)
s = Service(CHROMEDRIVER_PATH)

driver = webdriver.Chrome(service=s, options=options)
driver.get(URL)
 ```

### what if the connection is insecure? 
install this [certificate](https://raw.githubusercontent.com/wkeeling/selenium-wire/master/seleniumwire/ca.crt) 

- or get the certificate using: `python -m seleniumwire extractcert`


after the certificate is installed,

1. open chrome settings
2. select "Privacy and Security"
3. under "Advanced" setting, click "Manage device certificates"
4. then, click "Trusted Root Certification Authority" -> "import"
5. import the certificate you just have downloaded.


this will make the connection secure. 

