## Selenium-recaptcha-solver

You can use this package to solve ReCAPTCHA challenges with selenium.

It supports single-step and multi-step audio solving for ReCAPTCHA V2 with >90% success rate.

Please use this package responsibly and for non-exploitative ends.

## Requirements 

Python 3.7+

Main dependencies:
<ul>
    <li>SpeechRecognition python package to transcribe speech</li>
    <li>Pydub for file conversions</li>
    <li>Requests for HTTP requests</li>
    <li>Selenium for web driver </li>
</ul>

If you're getting an error related to FFmpeg not being installed or in your PATH, get it here: https://ffmpeg.org/download.html

If the error persists, make sure FFmpeg is properly installed for your OS and in your PATH.

## Installation

```bash
python -m pip install selenium-recaptcha-solver
```

## Usage example with ReCAPTCHA demo site

```python
from selenium_recaptcha_solver import RecaptchaSolver, StandardDelayConfig
from selenium.webdriver.common.by import By
import undetected_chromedriver as webdriver
import pytest


test_ua = 'Mozilla/5.0 (Windows NT 4.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36'

options = webdriver.ChromeOptions()

options.add_argument("--headless")
options.add_argument("--window-size=1920,1080")

options.add_argument(f'--user-agent={test_ua}')
options.add_argument('--incognito')

options.add_argument('--no-sandbox')
options.add_argument("--disable-extensions")

test_driver = webdriver.Chrome(options=options)

solver = RecaptchaSolver(driver=test_driver)

test_driver.get('https://www.google.com/recaptcha/api2/demo')

recaptcha_iframe = test_driver.find_element(By.XPATH, '//iframe[@title="reCAPTCHA"]')

solver.click_recaptcha_v2(iframe=recaptcha_iframe)
```

You can check a detailed use case in the tests folder of this project (Its execution is shown below in the demonstration chapter).

## Demonstration
[![Image from Gyazo](https://i.gyazo.com/858ceb5df9f43f6aafadf69e233cd2d1.gif)](https://gyazo.com/858ceb5df9f43f6aafadf69e233cd2d1)

## Avoiding detection

To decrease your chances of ReCAPTCHA detecting automated queries, try the following:
- Use a custom user-agent header (Make sure it's not a headless user-agent!)
- Use a hard-to-detect web driver (Good example: https://github.com/ultrafunkamsterdam/undetected-chromedriver)
- Use proxies to avoid IP blacklisting

An example of a good user-agent: Mozilla/5.0 (Windows NT 4.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36

An example of a bad user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) HeadlessChrome/92.0.4512.0 Safari/537.36

Note the last part of the user-agent; the headless specification is usually there.

## Questions
If the documentation hasn't covered something, or you have questions about how to use the package or how it works, please reach out.
