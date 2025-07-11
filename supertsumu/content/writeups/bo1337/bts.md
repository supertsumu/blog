---
title: "Break the Storage"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## Break The Storage - 50 points - Web

<center><img src="/breakthestorage.png" width="63%" height="63%"></center>

We get sent to a website with a username and password input field:

<center><img src="/inputfields.png" width="63%" height="63%"></center>

Trying to log in with incorrect credentials will trigger this pop-up:

<center><img src="/popup.png" width="63%" height="63%"></center>

Upon inspecting the source code of index.js?v=1337, We can see that upon successful login, we will be redirected to profile.html. Going straight to profile.html will redirect you back to login.html if the correct credentials are not entered. I used Burp Suite’s proxy to intercept and stop the site from redirecting me to login.html when I get to profile.html. After inspecting the sources of the page, we can find the flag in profile.js:

<center><img src="/btsburp.png" width="100%" height="100%"></center>
