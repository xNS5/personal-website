+++
title = "UML Class Editor"
description = "An Android application for creating UML diagrams."
draft = false
date = 2022-03-01
[extra]
tech = "Java, Android"
repo = "https://github.com/xNS5/UmlClassEditor"
logo = "uml.png"
alt = "The UML Project Logo, a picture of boxes connected by lines."
+++
---
## About UML Class Editor

I came across this project while browsing [FOSSdroid](https://fossdroid.com/). After I took an OOP class, I realized
the importance of planning out a project before coding it up. In a project with lots of moving parts, I found that it
was helpful to draw out classes, their attributes, public/private methods, how they should interact, and to use that
as a "to do" list of sorts. Nothing beats pen and paper, but I had recently purchased a Samsung tablet that came with a stylus, and
I wanted to take advantage of that. I found websites like [Draw.io](https://draw.io) incredibly useful, but it wasn't compatible
with tablet devices. I really like the tactile experience of interacting with an application or website, so finding
something similar to Draw.io for an Android tablet was a challenge. I found that the application suited my purposes perfectly,
however I had a few issues with it. First and foremost, the application toolbar/menu bar color irritated me. It initially
was a bright purple, which was a bit of an eyesore. Functionality wise, the menu organization wasn't the most intuitive, it had no 
icons, and there were some bugs related to saving data. 

I had experience working on 2 mobile applications, so tracking down the bugs was fairly easy. All I had to do was set a breakpoint
and replicate the actions that caused the application to crash.

## Thoughts

This was a great application, but I had some issues with the way it was initially coded. Firstly, the author didn't wrap file/data operations
in `try(){...}catch(){}` blocks, which is why the application was crashing initially. I was trying to run a delete operation when I had no saved projects
which threw a `NullPointerException()`, causing the application to crash. That was an easy fix. The next issue I came across was that the application
used a deprecated API for loading/exporting data, [`onActivityResult()`](https://developer.android.com/reference/android/app/Activity#onActivityResult(int,%20int,%20android.content.Intent)). 
This wasn't causing the crash, but it was something that needed to be addressed. This took a bit more time to figure out as I didn't fully understand what it did, and how to implement the correct API, 
[`registerForActivityResult()`](https://developer.android.com/reference/androidx/activity/result/ActivityResultCaller#registerForActivityResult(androidx.activity.result.contract.ActivityResultContract%3CI,%20O%3E,%20androidx.activity.result.ActivityResultCallback%3CO%3E)).


## Roadmap

I have a few ideas for how to make this application better, at least for my purposes. 

* Color customization. I like to be able to choose the theme of the applications I use, like in [Slide for Reddit](https://play.google.com/store/apps/details?id=me.ccrama.redditslide) for example
and I'd love to add that functionality to this application. 
* Exporting to different file types. Currently the data exports to .html files, which isn't the most practical when it comes to sharing files with others. I intend to create options to 
export the diagrams to PDF and possibly JPG/PNG formats. 
* Cloud Storage integration. A lot of applications like this have the ability to sign in with a cloud storage account such as Google Drive, One Drive, Dropbox, etc. and I want to add that functionality
to this application as well. 
* Sharing diagrams as PDF/JPG/PNG to either email or some sort of messaging platform. Software development is a highly collaborative profession,
and adding this feature will make this more functional.