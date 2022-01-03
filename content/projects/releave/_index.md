+++
title = "ReLeave"
description = "A cross-platform mobile application designed to aid a person going through Cannabis abuse recovery."
template = "project.html"
draft = false
[extra]
tech = "Flutter (Dart), SQlite"
repo = "https://github.com/xNS5/ReLeave"
logo = "releave.png"
alt = "The ReLeave project logo, a series of colored blocks forming the letter R."
+++

## About ReLeave

I came up with this project over the summer of 2020. I had discovered the [/r/Leaves](https://reddit.com/r/leaves) subreddit, and it occurred to me that there may
not be many applications out there specifically for cannabis abuse. Most applications I came across were a one-size-fits-all type application that
attempts to work for anyone, applications for alcoholics, people who are dependent on opioids, but not many applications for cannabis dependency.

Society is chomping at the bit for cannabis legalization in the US. Often times people talk about the wonders that the plant can have on a person's body, how it
can help people undergoing chemotherapy, treat depression, anxiety, etc. however people don't often talk about cannabis dependency and the effects it can have on a person.

I had fully intended to create this application on my own, but I saw an opportunity to create this in a class called "Technology for Social Good". We were asked
to come up with a project idea and pitch it to the class. I made my pitch, and a few other students also thought that this would be a great project to work on. I decided to do this project in Flutter because technology is always a limiting factor for people. Some peopne can't afford the newest iPhone or the highest-spec
Android device, so it had to be friendly with most newer OS versions and not be resource-heavy. As a perk, this language is very friendly toward new users and is well documented.

This application has the following features:  
- Mood/Craving tracking.
- Journaling system.
- Custom goal creation.
- Tracking features.
- A badge system that awards the user whenever they reach a milestone (e.g. staying *x* days sober, saving *x* dollars by refraining from consuming cannabis products, etc.)
- Interacting with a community of people who are also attemtping to maintain sobriety.


  <img class="project_screenshot_mobile_right" src="/images/releave_home.jpg" alt="Releave Home Screen with two buttons: one blue button with the words 'Community Check-In', and one green button with the words 'Personal Check-in'. In the top
  right corner are the words 'Days Sober: 366' indicating that the user has been sober for a year and one day."/>

While this is purely anecdotal, many of the posts I've seen on [/r/Leaves](https://reddit.com/r/leaves) involve a lot of self reflection. People talk about behaviors they developed as a result of their dependency, how they treated others, missed opportunities, and how they felt that day after being sober for an extended period
of time. To aid with that reflection, we decided to implement a Mood/Craving tracker system which allows them to reflect back on their day. They will have the
option to rate how they're feeling on a scale from 1-10, and create a journal entry for any thoughts or feelings they have that a simple rating can't describe.

Also included are a few tracking features: the first is a sobriety tracker, measuring the number of days since the user started their journey; the second
is a money tracker. When the application is installed for the first time, the user would be asked how much money they spent on cannabis products, how much they
consume, and the method of consumption. The money tracker will calculate how much they've saved based on that inputted information, as well as how much they've
refrained from consuming. 

The badge system is an attempt to "gamify" the application -- to make the user want to maintain their sobriety, not dissimilar to the coins used by Alcoholics
Anonymous but in this case digital and more than just maintaining sobriety for a set amount of time.

There are a lot of habit tracking applications out there that could be used to help with a person recover from substance abuse. However, many applications are missing a key feature: a community. It's not uncommon for support groups to hold meetings so members can share experiences, support others, and to not feel alone during
recovery. Many existing applications have a self-hosted platform for users to interact, but a downside of that especially for a new application such as ReLeave is
getting enough users on the platform in the first place. Instead of building out a platform for users to interact, I had the idea to instead leverage Reddit's [/r/Leaves](https://reddit.com/r/leaves) community.

<img class="project_screenshot_mobile_left" src="/images/releave_rating.jpg" alt="The picture contains a checkbox with the caption 'Did you refrain from using cannabis today?' with a box below that for the user to tick, and 7 sliders corresponding to feelings such as happiness, sadness, craving, for the user to rate their feelings at that given time." />

## Technologies Used

Flutter was chosen because, as mentioned before, it's a framework that can transpile code into code that can be run on both iOS and Android devices, 
allowing people with any device to use it. Reddit is already designed for users to communicate, has a free API that I could leverage, and I wouldn't have to manage 
another system and deal with user account issues. To achieve this, we used the dart package [Draw](https://pub.dev/packages/draw) or Dart Reddit API Wrapper to 
interact with the subreddit. Data is stored in a local SQlite database, using a custom schema. 

The journaling feature can either save the data to local memory or to post to the [/r/Leaves](https://reddit.com/r/leaves) subreddit, provided they already have
an account.

<img class="project_screenshot_mobile_right" src="/images/releave_leaves.jpg" alt="A screenshot of the Reddit feature, listing off posts from users of the /r/Leaves subreddit." />

## Thoughts

This was my first project where I felt satisfied at the completion of the course. Flutter made this application very easy to throw together, and working with
a team that was motivated and had a vested interest in this project made this an incredibly enjoyable experience. Technology wise, the features are in place
however they're not the prettiest and the database is quite frankly a mess. I designed the database, but looking back I really didn't know what I was doing. 
I plan on reviving this project and pushing forward with it now that I have the time, the application is in dire need of a facelift and some stylistic 
standardization, as well as a complete database overhaul.

This application was my first mobile application that I've ever worked on, and I plan on seeing it to the end and get it published to both iOS and Android app stores.
