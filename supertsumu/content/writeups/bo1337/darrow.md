---
title: "Darchrow"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## Darchrow - 100 points - Misc

<center><img src="/darchrow.png" width="75%" height="75%"></center>

We get the following image from this challenge:

<center><img src="/darchcipher.png" width="100%" height="100%"></center>

Instead of using OCR software to get the text out of the image, I meticulously typed the letters for the sake of accuracy:

> ACZQQOKLHUALHPTXGXKEPWTLDJUCEORHRKTQRTVKXOWRBYACBUKRUPCEA QRAKMZRJHCEHZJWJKSGTLTMOXTEJHLPPEHXJBQQWKXYQNKFTOKBJUVFRUF CSQMTXHTTDJSOFWHYNSOHVEZGQVURJFJALJEXQWWYWIZBJLMOYDMGNXOMR MLQRSYWZHJGBLCSHNMYFXESJNFBBITRXHKZYQGYIPEUYTNFXSSPCXIZJMR CTLHUUHBFEXIVBMEURYMPAZATXUVNVQRSLPFVWWBBUHOEMXYRPMLTYZXLH SAPMMMQOEHXKQCDWBSWDMTFMSMFBNCQGMQHHJPQYKJPZNMYYDKZYZXUHOO HAIAFGMDBMYAEQPRSUVQKGEZSA

Looking up “Darchrow consumer of worlds” on the web, we can find a Dota 2 character named Darchrow, the Enigma. I immediately placed the ciphertext into [dcode.fr’s enigma decoder](https://www.dcode.fr/enigma-machine-cipher):

<center><img src="/enigmadecode.png" width="90%" height="90%"></center>

After adding spaces to the output, we can find the flag:

THE FLAG IS BOBRACESENIGMAFORALANTURINGBRACES

#### Flag: BO1337{ENIGMAFORALANTURING}