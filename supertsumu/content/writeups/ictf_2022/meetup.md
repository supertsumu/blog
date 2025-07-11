---
title: "The Meetup"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## The Meetup - 150 points - OSINT

<center><img src="/The_Meetup.jpg" width="100%" height="100%"></center>

### Description

My agent just sent me this image as the location for our next secret meetup. Where exactly is this?

(This question does not use the BAT22{} flag format. Answer with the exact street or building name this image is taken from.)

Creator: Nicholas Mun

<br/>

### The Writeup

In this challenge, we are given the image file named The_Meetup.jpg. You can download this file [here](https://drive.google.com/file/d/1Nx_Uu0Q_f1M_reVHWbzwQJpuYRR7zZ_L/view?usp=sharing).

The goal of this challenge is to find the exact name of the street name or the building name of the buildings in white.

I always though people who were able to determine locations from mere images were really smart and I highly respect them. I’ve came across my handful of this type of OSINT questions but I’ve never been able to solve them until I had seen the amount of attention of detail used to solve these questions from writeups. Today, I managed to solve my first question of the sort, to say the least, I was ecstatic (for a whole 10 minutes). Here is my thought process on how I managed to solve the challenge:

I use the flag to find the flag. The first notable clue I found was in the middle of the image, a red flag highlighted by the white balcony that it was hanging off on. Zooming in, I confirmed it to be the Turkish flag:

<center>
<img src="/balconyflag.png"><img src="/turkishflag.png" width="250px" height="175px">
</center>

The next clue I found was the name of a building by the hill on the top left side of the Image:

<center><img src="/comukres.png" width="100%" height="100%"></center>

Googling “comu kres turkey” brings us to their Facebook page. The building on their home page looks similar enough with the one on the image. It looks like its a kindergarden. In their about tab, I found a link to their location on google maps. You can find the location to the area here.

Taking a look at the buildings surrounding Comu Kres, I was able to find other locations that match the landmarks of the image. The 3 most notable other than Comu Kres being:

* The huge mosque with its distinct pointy pillars:
<center>
<img src="/mosque.png">
<img src="/mosque2.png">
</center>

* And Hotel Zileli I recognised from this neon sign on the rooftops at the right side of the image:

<center>
<img src="/zilelisign.png">
<img src="/zileli.png">
</center>

Now that I had mapped out 3 landmarks on the left, middle and right of the image, it is only logical that the position that the picture was taken is diagonal to the line crossing Comu Kres, the mosque and Hotel Zileli:

<center><img src="/mapimage.png" width="100%" height="100%"></center>

The buildings painted in white with the pool that takes up half of the image is most likely a hotel or a condominium complex. Another detail I noticed was that there was a 2 lane highway in front of the hotel/condominium. Piecing it all together, the place we are looking for is either Kolin Hotel or The Ataol Troya Hotel located in grey oval on the top of the image above.

**Flag: Kolin Hotel**