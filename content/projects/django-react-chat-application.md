+++
title = "Django/React Chat Application"
description = "A Full-Stack chat application "
template="project.html"
draft = false
date = 2022-07-19
[extra]
tech = "ReactJS, Django, REST"
repo = "https://github.com/xNS5/django-react-chat-app"
logo = "python-file-symbol.png"
alt = "A picture of a digital file, with a black bottom border with the letters PY representing the Python programming language, and on top is the Python logo consisting of two snakes intertwined."
+++

## About the Application

(Please shoot me an email to request access to the application. Considering this was part of a job application I'd like to keep this project as low-profile as possible.)

This project was given to me as a part of a project-based interview through a third-party hiring company. This was one of the first "interviews" I participated in, and gave me some enlightening
experiences and insights into what I needed to improve upon as a developer. I was added to a Slack channel with a number of other developers who would be helping me through the interview.
I was assigned 3 tasks that I was expected to accomplish within ~2 weeks or so. I've interacted with Django before, but React was totally new to me. The tasks were: Fix the application 
such that two clients can send messages to each other, Add a "read receipt" feature, and redesign the database to allow for 3...n users to share a conversation (i.e. have a group conversation).

### Issue No. 1 -- Message No Go

These issues were spread out between both the backend and the frontend applications. When a user sent a message to another user, the messages weren't showing up in the receiving user, and when the user
refreshed the page the messages appeared -- but they weren't in descending order. After doing some poking around, I found that the messages were populating the backend database, and were successfully being sent to
the receiver, but they weren't appearing in the receiver's conversation. I concluded that the messages weren't appearing due to React's state hook not updating. The backend fix was much easier than the frontend fix;
I just had to flip some variables around. 


### Issue No. 2 -- "I read that..."

This feature was a bit harder to implement. I've used chatting applications with read receipts for a large chunk of my life, but I had no real idea how to go about implementing it. I looked at a few existing
platforms, like Facebook Messenger and Signal. With Facebook Messenger, the read receipt is the other user(s) profile pictures. With Signal, the read receipt has 3 steps: Sent, Delivered, and Read. This would
require the server to send 3 total signals to a client: one that the server has received the message, that the server has successfully delivered the message, and that the receiving client has read the message. 

Both applications more or less behaved the same, server differences aside. Whenever a client clicked on a conversation with unread messages, the messages were updated to reflect that the message(s) were read.
I opted to model this feature after Facebook Messenger's behavior to reduce the amount of work on my part. Then came the hard part.

The database was designed such that a conversation can only exist between two users. There could only be one unique combination of two users that make up a conversation. Each message sent belonged to a conversation.
I initially thought that the easiest way to implement this was associate the users `userId` to a particular message, denoting that `user` has read the most recent unread messages in the conversation. After some thought,
I realized that I could actually accomplish this by instead representing the read receipt as a `boolean` in the database and use client-side logic to display the correct read receipt. If the most recent message
is from the other user, it's assumed that they've read the conversation up until that point. If the message is from the current user and the message is marked as unread, then the other user hasn't read the conversation.
If it's marked as read, then the read receipt should be moved to the most recent message. 


### All Aboard the Struggle Bus

The two major issues I faced with this step was that I hadn't ever messed with [Websockets](https://socket.io/), and that I didn't really understand what it meant to ["deep copy"](https://stackoverflow.com/questions/48710797/how-do-i-deep-clone-an-object-in-react) a conversation.
I was given the hint to modify the websocket, but it didn't really click what that meant. I was so hooked (so to speak) on the frontend application, that I didn't think to check the backend for an *actual* websocket application. That was the biggest
blocker for this ticket -- I wasn't able to make any meaningful progress because I was unable to test the application. 


### Issue No. 3 -- Redesign Everything

This last issue was to redesign the database such that it allowed for group conversations. A group consisted of 2...n users. This meant that the read receipt notification would need to be updated such that each
user would have their own read receipt in a conversation. My line of thinking was (and still is) that I could modify the database such that it could allow for 3...n users without having separate tables for conversations
between only 2 users. Each conversation would be held between a "group" of users. This "group" could be 2...n users. Each "group" would have a conversation, and each conversation would have 1...n messages. Having this concept
of group membership would also allow for group permissions, like the ability to add/remove users from the conversation for example. 


## Thoughts

All in all this was an interesting experience. This was the first time I've worked on a larger project in a more professional context. While it did show me my strengths and weaknesses, I can't help but
feel a bit disappointed by this experience. There were at times some issues with communication between myself and the reviewers. When I tried to ask follow-up questions to clarify any concepts that didn't make sense,
they often went unanswered. My implementation for Issue No. 2 took me a bit more time than I anticipated due to completely skipping over the websocket folder in the backend server. I opted to continue working on the project
because I was led to believe that the company I was applying for had a hiring freeze in place, and I could continue working on the application without penalty. After I completed the project, I heard nothing back
about whether I was still being considered as a candidate. 

One piece of feedback that I was a little shocked by was that I didn't communicate often enough. Looking back through the messages I sent, I realized that there was some truth to this. I have a habit of getting engrossed
in projects, and I believe that's what resulted in my less-than-stellar communication. In my past jobs I was used to having either remote or face-to-face meetings. Communicating solely over messages
was very easy to forget. It was hard to accept that I could have done better, but this was most definitely a reality check for me. I knew that I was going to be constantly learning
when I started working, but communication wasn't something that I thought I needed to improve upon.

In retrospect, while I did learn a great deal about React, Django, and REST API's, I can't help but feel like my time could have been better spent brushing up on 
Computer Science fundamentals in preparation for interviews.