+++
title = "reCAPTCHA Validator"
description = "A small FastAPI server to validate the responses from a reCAPTCHA challenge."
template = "project.html"
draft = false
[extra]
tech = "FastAPI, Python, Javascript,  Heroku/Azure"
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
but I don't need anything super big that has a lot of requirements, configurations, yada yada yada. FastAPI fit the bill perfectly. I just wanted something lightweight to send `POST` requests to the Google API endpoint that didn't expose my reCAPTCHA secret key client side. 

## Technologies Used

Simply put, I used a FastAPI backend server, a javascript function located in my [personal website](https://www.michaelkennedy.dev/contact/), and Heroku to host it. I opted to use Heroku 
because I was at least moderately aware of it and how to use it, but I think I'm going to migrate it to Azure as I have ~$100 in credit thanks to being an (ex) student. 

## Thoughts

I hate [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).

This project took me less than 24 hours to throw together in total. Someone in a local
Discord server mentioned that they were experimenting with FastAPI, and given the scale
and impact of my needs I thought it would be a fun, quick project to throw together. 

