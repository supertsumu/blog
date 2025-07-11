---
title: "When_universes_collide"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## When universes collide - 50 points - Forensics, Cryptography

We are given this file [Challenge 1.png](https://drive.google.com/file/d/1F06LfUR5PaErV9L6DEdY9RBOEKn374Hk/view?usp=sharing).

Instinctively we would all scan this qr code. We get this string in return:

```
otp!áth:,+totp/No~d%20AccÏ%nt:vuctf2>2Ò@b¥s{paâa$iÚeîcÏm?algïrn|hc=SHA1&digiws=6.issuå}=No}d+AcCounz&.e~ißd=30%sek"åt=6ZZKUEJDOVFYC4OIQBU2PLPYBH54VXWB
```

We spent some time thinking what this could mean. But the qr code and its resulting string was actually bait. To actually get the flag we placed the qr code image in stegsolve. After going through a couple of planes we found this:

<center>
<img src="/qrbinary.png" alt="qrbinary">
</center>

I was overjoyed, to say the least when I found the above resulting image. My teammate g3nj1z plugged the image into OCR software which got us the following binary:

```
01100111011011100110100101101000011101000111100101
11001001100101011101100100010101011111011001000110
11100110000101011111011001010111001101110010011001
01011101100110100101101110010101010101111101100101
01101000010101000101111101100101011001100110100101
00110001011111011001100110111101011111011011100110
11110110100101110100011100110110010101110101010100
01010111110110010101110100011000010110110101101001
011101000110110001010101001011010011001000110100
```
We encoded it into text with CyberChef and got the string:

```
gnihtyrevE_dna_esrevinU_ehT_efiL_fo_noitseuQ_etamitlU-24
```
Reversing the string gives us our flag.

Flag: 42-Ultimate_Question_of_Life_The_Universe_and_Everything

