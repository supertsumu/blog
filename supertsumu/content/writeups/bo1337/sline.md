---
title: "Streamline"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## Streamline - 176 points - Networking

<center><img src="/streamline.png" width="63%" height="63%"></center>

We are given an image file, this time named LamboRidzuan:

<center><img src="/lamboridzuan.png" width="63%" height="63%"></center>

Using [stegseek](https://github.com/RickdeJager/stegseek), I am able to bruteforce a hidden file using rockyou.txt.

<center><img src="/stegseek.png" width="70%" height="70%"></center>

Now that we have Ridzuan’s handshake, we can try to crack his wifi password. Using [Mentalist](https://github.com/sc0tfree/mentalist), I created multiple wordlists in the format of 4 alphabets and 4 numbers separated by a symbol. I cracked the handshake using hashcat and the wordlists:

<center><img src="/crackhandshake.png" width="70%" height="70%"></center>

I managed to get the password oyen@9367 which was the flag for the challenge.

#### Flag: oyen@9367

