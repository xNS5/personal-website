+++
title = "WWU Accessibility Engine (ACE)"
description = "A full-stack accessibility automation tool developed for Wandke Consulting in Bellingham, Washington."
template = "project.html"
draft = false
[extra]
tech = "Javascript (Vue/Sails), HTML + CSS, Python"
repo = "https://github.com/xNS5/Axe-Core-Enhancements"
logo = "accessibility.png"
alt = "WWU ACE Logo -- An Accessibility symbol of a person surrounded by a circle."
+++

## About ACE
This is my capstone project during my senior year at Western Washington University. I led a team of 4 in the development of an accessibility testing program for Daman Wandke of [Wandke Consulting](https://wandke.com/), an accessibility consulting company
in Bellingham, WA. My team and I spent a year working on a full-stack application to streamline their website accessibility evaluation process. Initially, they used Deque Labs' aXe browser extension to determine whether a given webpage conforms to the World Wide Web Consortium's
Web Content Accessibility Guidelines (WCAG). From there, they manually entered the data from the accessibility scan into a CSV file, added some comments such as information about the specific WCAG violation, how to remedy that specific violation, and any other relevant notes. In addition
to aXe, it was requested that we also integrate [Crest](https://github.com/vmware/crest) by VMware -- another accessibility testing engine. This is another python-based engine, so the project may need to be refactored to include some sort of python server to run both the spider and Crest.

## Technologies Used
This project uses Sails.js as the backend server, Vue.js as the frontend application, Selenium Webdriver to manipulate installed browsers, and Python to gather sub-pages of the inputted website to use as input on an accessibility scan. Initially the requirements included
two applications, one to run the accessibility scan and one to edit the results of the scan prior to exporting it to a CSV or PDF file. After analyzing the requirements, our client decided that simply retuning the results in a CSV format -- removing the need for a second
application.  

The backend server is able to run independently of the frontend, and vice versa. To stress test the backend, I wrote 15 bash shell scripts to send POST requests containing different configurations. These configurations included 
different lists of websites, different WCAG conformance levels, browser resolutions, and whether to spider a website for a given URL. At the moment it only supports Firefox and Chrome; we considered adding MS Edge to the list of testable
browsers, but ultimately we decided against it as both Chrome and Edge are chromium-based so the results would be the same for both browsers.

Integrating the spider was by far the most challenging aspect of this project. It would have been easier to simply use a Javascript web scraper, but there are more robust Python libraries that had the functionality I was looking for.
There are some Javascript libraries for running Python scripts, but our use case is unique enough to where I had to dig deep into forums and documentation to figure out how to make the python script is callable via POST request.  

## Thoughts
This was an interesting project. This was the first time I've considered the accessibility of my projects and the web in general. Both in passing and in a digital accessibility class, I learned about a case against [Dominoes Pizza](https://www.cnbc.com/2019/10/07/dominos-supreme-court.html)
where a man filed a lawsuit because their website didn't conform to WCAG AA guidelines. It even went all the way up to the Supreme Court. I always assumed (incorrectly so) that big companies such as Dominoes ensured that people of all abilities could use their website and applications.

This was the first time I took on a long-term project for an actual client and not a professor. I learned a lot about maintaining a professional relationship with someone outside my school, communicating with them on a regular basis to give updates on the status of projects, and leading a team. 
We decided to use a [Kanban](https://www.atlassian.com/agile/kanban) methodology for developing this project because the vast majority of features that were requested were backend-heavy, so doing scrum-style sprints wouldn't have been the best fit. Once the core features were connected and functional,
we arranged a meeting with our client or sent an email with example output. Often times the email would be the more effective means of communication, as it gave them time to evaluate and think about what's been done so far and if any new features should be added.

Most of the time features came to fruition through trial and error. Integrating the Spider functionality for example took a significant amount of time researching and testing to implement. The biggest issue that I ran into was determining how to run the spider on both Unix and Windows operating systems.
I falsely assumed that if I created a virtual environment folder for just a *nix system it would work for any system. After one of my teammates attempted to run it on their Windows computer, errors popped up. I had to spin up a Windows 10 virtual machine to install and test our project, and I found that:

1. For some reason Windows 10 is missing a few features which prevents python from installing Scrapy -- the library we used to scrape for subpages of a website. 
2. Python on Windows 10 has a different virtual environment structure, so checks needed to be added to ensure that the right environment was used whenever the spider is run.


## Demonstration

[![Youtube Video Preview of the WWU ACE project video](http://img.youtube.com/vi/pBowDT5dDmA/0.jpg)](http://www.youtube.com/watch?v=pBowDT5dDmA "WWU ACE Demo Video")
