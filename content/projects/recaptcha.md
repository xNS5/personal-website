+++
title = "reCAPTCHA Validator"
description = "A small FastAPI server to validate the responses from a reCAPTCHA challenge."
template="project.html"
draft = false
date = 2022-03-01
[extra]
tech = "FastAPI, Python, Javascript, Microsoft Azure"
repo = ""
logo = "captcha.png"
alt = "A captcha icon of 3 arrows forming a circle."
+++

## About ReCaptcha

According to [Google](https://www.google.com/recaptcha/about/):

>  reCAPTCHA uses an advanced risk analysis engine and adaptive challenges to keep malicious software from engaging in abusive activities on your website. Meanwhile, legitimate users will be able to login, make purchases, view pages, or create accounts and fake users will be blocked. 


I wanted to integrate reCAPTCHA into my website, specifically in the "Contact" form. Once it was successfully tested and added to the contact form, Google informed
me that I wasn't validating the responses and linked the relevant documentation page. When wracking my brain for 
possibilities, I remembered that [FastAPI](https://fastapi.tiangolo.com/) existed. I could have used Node for example,
but I don't need anything super-big that has a lot of requirements, configurations, yada yada yada. FastAPI fit the bill perfectly. I just wanted something lightweight to send `POST` requests to the Google API endpoint that didn't expose my reCAPTCHA secret key client side. 

## Technologies Used

Simply put, I used a [FastAPI](https://fastapi.tiangolo.com/) server, a javascript function located in my [personal website's contact form](https://www.michaelkennedy.dev/contact/), and an Azure application to host it. I initially opted to use Heroku as I already had an account, 
but I thought that I'd use the Azure student credits I had accrued. Migrating my code from Heroku to Azure was painless, and I learned a bit about how to navigate the Azure dashboard. After some light testing, I found out that after
20 minutes the validation server powers down -- a policy set by Azure for free applications. Going with a paid plan would mean that I wouldn't have to deal with that policy, however there were a few downsides. The biggest issue is that I don't have a regular source of income.
This application isn't doing anything incredibly expensive computationally, so it ultimately may be much cheaper to run than I initially thought. That said, I'd rather not have to spend money to find out that my application requires a lot of computing time. Secondly, the memory requirements
for this application are pretty low to begin with. It can easily do its job on the free tier plan, and frankly hasn't even made a dent in the daily quota. 

And that brings me to the issue of the application powering down. After a bit of thought, I realized that it's shutting down due to inactivity after 20 minutes. In order to prevent inactivity, I needed to find a way to keep it awake. If my print server VM had enough space (it's running
on a little rinkydink Surface 3) I could easily just set up a [CRON job](https://ostechnix.com/a-beginners-guide-to-cron-jobs/) that sends a `GET` request to the reCAPTCHA validator to make sure it's still alive. After a bit of googling, I discovered [cron-job.org](https://cron-job.org/en/).
It's a service that essentially acts is as if I created a [CRON job](https://ostechnix.com/a-beginners-guide-to-cron-jobs/) on a local computer and let it do its thing. While it works, I was curious whether I could replicate the behavior in an Azure application. 

Turns out I could! I created a [Function Application](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview) which runs a python script on an interval. I set the interval to run every 15 minutes, however I think I may change it to 18 minutes to minimize the number of requests made.
While there were a few road bumps like not having the `.ssl-key.log` file added as an environment variable to my `.zshrc` file for some bizarre reason, the fix was relatively quick and easy to implement. I'll be monitoring both applications to see how this fix affects the free tier's daily quota. 

## Thoughts

### FastAPI

I hate [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS). While I'm sure there's a very sound and logical reason to have it, the errors I usually get with CORS don't really explain how to *fix* my issue.

This project (along with the CRON project) took me less than 24 hours to throw together in total. Someone in a local Discord server mentioned that they were experimenting with FastAPI, and given the scale
and impact of my needs I thought it would be a fun, quick project to throw together. 

### Azure

Azure's documentation needs a bit of work. I was initially hoping to make an application with a few different endpoints for testing purposes, but as it turns out Azure function applications don't support that behavior. This reminds me of some issues I was having with
[Windows' Assigned Access](https://docs.microsoft.com/en-us/windows/configuration/guidelines-for-assigned-access-app). While I was working in the Viking Union, I was tasked with creating a kiosk device. I wanted to use Assigned Access to achieve this, but I also required
the use of a specific browser extension. As it turns out, Assigned Access doesn't support browser extensions and this information was [buried in the Microsoft documentation](https://docs.microsoft.com/en-us/deployedge/microsoft-edge-configure-kiosk-mode#functional-limitations).

The documentation on creating Azure applications is unnecessarily spread out and at times cryptic.

Had I stayed with Heroku I probably would have the same issue where free-tier application goes to sleep after a set amount of time. Odds are I would have come up with a CRON-like solution to keep it running. That said, Heroku's dashboard is significantly friendlier compared to Azure. Many
of the settings are pretty self-explanatory whereas compared to Azure -- for example, an App Service has a few tabs which allude to the same function such as "Activity Log", "Logs", "App Service logs", "Log Stream". End of the day I really just switched to Azure because odds are I'd be working
with it in a professional environment. Heroku, Azure, Digital Ocean, they'll all get the job done. 
