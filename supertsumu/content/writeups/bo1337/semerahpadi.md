---
title: "Semerah Padi"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## Semerah Padi - 100 points - Networking

<center><img src="/semerahquestion.png" width="63%" height="63%"></center>

We open the flaghere.pcap file in Wireshark to analyze the packets. We can find some http packets with Lorem ipsum as the content. We can view the whole conversation by following the tcp stream:


<center><img src="/loremipsum.png" width="100%" height="100%"></center>
Hidden within the Lorem Ipsum, we can find a suspicious string that resembles a scrambled web address:
<br/><br/>

<center><img src="/scrambledlink.png" width="63%" height="63%"></center>

After some time trying different transposition ciphers, using the rail fence cipher, we can get a valid url. The link brings us to this pastebin: https://pastebin.com/5WNzAUve

<center><img src="/matkilau.png" width="80%" height="80%"></center>

The second link gives us Semerah Padi.wav. Opening the file with sonic visualizer and adding a spectrogram gives us the flag:

<center><img src="/semerahpadiflag.png" width="100%" height="100%"></center>
