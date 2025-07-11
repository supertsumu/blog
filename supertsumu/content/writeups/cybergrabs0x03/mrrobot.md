---
title: "Mr. Robot"
date: 2022-12-28T18:07:47+08:00
---

[Home](/)

## Mr. Robot - 200 points - Forensics

Description:

Mr. Robot most famous TV show but least people know about it.

Flag Format: CYBERGRABS{}

Author: Tech Wizard

This forensics challenge comes with the file chall.wav.

Listening to the file and reading the title, this seems to be a monologue from the American tv show Mr Robot.

Solution:

I googled “mr robot wav files” which pointed me to this site which writes about a tool called DeepSound that was used in the tv series. DeepSound is a steganography tool used to hide data/files in wav files. This is done by by changing the LSBs (Least significant bits) of the cover audio file which will not change much of a difference since the least significant bits only brings little insignificant changes to an image/audio file.

Tools like DeepSound store data in the LSBs of the cover file. To extract the data, we must collect the LSBs of each byte of the file and merge them into actual data. DeepSound also has a function that allows us to extract hidden data from these files.

Unfortunately, the challenge file provided was too big for DeepSound to handle so we have to resort to other programs to extract the data.

After some digging, I found wavsteg which serves the same purpose as DeepSound but as a command-line tool. wavsteg requires a bit-count as an argument so that it knows how many LSBs to extract. We dont know how many bits we want to extract so we chose 1000 bits by random:

```bash
└─[$] stegolsb wavsteg -r -i chall.wav -o output.txt -b 1000                                                                                                                                         
Files read                     in 0.00s
Recovered 1000 bytes           in 0.00s
Written output file            in 0.00s
┌─[supertsumu@supertsumu] - [~/ctftools] - [880]
└─[$] cat output.txt                                                                                                               
CYBERGRABS{3VERY_8YTE_4RE_REAL_VALUE}
�'?D�Z�ϧiS[�PUUP�UU@TZꪪCj���"H�-��UV�TUPUUUꪯUVOꪓT�9�,\I�_���@
��$Q:/���1|?ƾUT�<<?U[�Py^C,ȎA넰�tPV��/ꓱm�y4����y"ÕP->Z�UUUUUPꪪj�O��h�� I;��RynO>��?$ߑWoYo8_M"A�Z�P??�U@?�qΈ�ƻL��&۽�er!���UP?��?Tl��rB��Ma8
*�N!l9��VUUU@?UU�P*+���-
�UT>P�(�??~v`w;�P��o1   HY^�C
                     �Lw�；T�VUUZM 1�_Qx��~|�ꝤĜP=�cS�P?�%
```

Flag: CYBERGRABS{3VERY_8YTE_4RE_REAL_VALUE}