---
title: "Torrent Analyze"
date: 2022-12-28T18:07:47+08:00
draft: false
---

[Home](/)

## Torrent Analyze - 400 points - Forensics

Description:

SOS, someone is torrenting on our network.

One of your colleagues has been using torrent to download some files on the company’s network. Can you identify the file(s) that were downloaded? The file name will be the flag, like picoCTF{filename}.

Hint: The file in question ends with .iso

We are given a pcap file. Open the file on Wireshark to get started!

First, we have to enable to bittorrent plugins for wireshark to recognise bittorrent packets. Click Analyze > Enabled Protocols, then search for “torrent”. Enable all bittorrent related plugins:

<center><img src="/plugin.png" width="110%" height="110%"></center>

Bittorrent uses udp to transfer data over the net. If we enter “udp” in the display filter, we can see all bittorrent traffic:

<center><img src="/infohash.png" width="110%" height="110%"></center>

Going through some of the packets, I found some BT_DHT protocol packets that contain hash values in the data. Looking up these hash values on the web might show some torrent sites with files available for download:

<center><img src="/hashfind.png" width="100%" height="100%"></center>

Going through a couple of these packets and reverse searching the hashes will bring us to a torrent site offering an Ubuntu disk image file (iso):

<center><img src="/tuxtorrent.png" width="100%" height="100%"></center>

The file name is the flag.

Flag: picoCTF{ubuntu-19.10-desktop-amd64.iso}