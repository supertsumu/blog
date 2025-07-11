---
title: "Snap"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## Snap - 100 points - OSINT


<center><img src="/snap.png" width="70%" height="70%"></center>

There weren’t many hints from this challenge other than it suggesting that the challenge remains on Instagram. Since the previous challenge is Instagram related, I took a look back at the challenge profiles and noticed that some of the profile images look very strange. Using [Toolzu’s Instadp](https://toolzu.com/downloader/instagram/instadp/), I was able to download the profile pictures from the previous challenge. Piecing them together gives us this full image:

<center><img src="/pieced.png" width="80%" height="80%"></center>

After some confirmation from the admins, the goal is to find the location of where this image was taken from. I sighted multiple clues that led me to thinking that this is in Malaysia. The most obvious being the navy & white building behind the brown one on the right is very similar to the ones seen in Malaysian police stations. The cars on the roads are also very common in Malaysia. After looking up some Malaysian trains, the one in the image looks very similar to the ones seen in the KL monorail mainly because of the stripe on the top of the train and the shape of the train. But the most obvious giveaway of the approximate location of the image can be found at the dome structure to the right of the image. Searching “domed structures in Malaysia” will give you a hard time finding that specific building in the image because of the multitude of domed mosques in the country so I made a guess and looked for “domed stadiums in Malaysia” and found Stadium Negara which matches the color and rough nature of the roof:

<center><img src="/stadium.png" width="100%" height="100%"></center>

Now, we have to find the exact location where the image was taken. According to the image, the camera seems to be floating next to a monorail near a station. I mapped out some stations near the stadium and started guessing the station name as the flag:

<center><img src="/googlemaps.png" width="100%" height="100%"></center>

Flag: BO1337{Imbi}