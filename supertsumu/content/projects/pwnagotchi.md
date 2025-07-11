---
title: "Pwnagotchi Build Guide (November 2023)"
date: 2023-11-25T11:45:01+08:00
---

[Home](/)

<h1 style="line-height: 1.2;">Pwnagotchi Build Guide (November 2023)</h1>
<center><img src="/pwnagotchi.jpg" alt="pwnagotchi" width="100%" height="100%"><br/></center>

The Pwnagotchi is an open source hacking mini war driving pet. It is inspired by the classic childer's toy tamagotchi. But instead of feeding it virtual food, it feeds itself with WPA handshakes and PMKIDs!

Hardware wise, the bare minimum you need to make a pwnagotchi is a Raspberry Pi Zero W, a micro usb cable and a micro sd card. However, you would only be able to run the Pwnagotchi in "headless" mode in this configuration without a screen. To make my configuration of the pwnagotchi, here is exactly what you need:

<ul>
<li><a href="https://my.cytron.io/c-raspberry-pi-main-board/p-raspberry-pi-zero-wh-basic-bundles">Raspberry Pi Zero WH (V1)</a></li>
<li><a href="https://www.waveshare.com/2.13inch-e-paper-hat.htm">Waveshare 2.13 E-Ink display (V4)</a></li>
<li>Micro USB Cable</li>
<li>Power bank</li>
<li>Micro SD Card (>= 8GB)</li>
<li>SD card reader/writer</li>
<li><a href="https://etcher.balena.io/">Balena Etcher</a></li>
<li><a href="https://drive.google.com/file/d/1BwrPqyn3g6ib0uJn736MVXJjOCQcbHg_/view?usp=sharing">Pwnagotchi Disk Image 1.5.5 Fix</a></li>
<li><a href="https://www.catalog.update.microsoft.com/Search.aspx?q=USB+RNDIS%20Gadget">Windows RNDIS Drivers</a></li>
<li><a href="https://www.thingiverse.com/thing:4511022/apps">3D Printed Case</a></li>
</ul>

There are alternatives for some of the hardware listed above but this is what worked for me. I am writing this blog so that people do not buy the wrong hardware that does not work. The official pwnagotchi website and the project itself has not been maintained since 2 years ago and some of the hardware recommended on the website are not for sale anymore. I have spent a lot of money testing multiple solutions with different hardware and this is the combination that works flawlessly. All the hardware should be able for purchase the time of writing of this and the links above are where I have bought them from.

The 3D printed case is just for aesthetics and light protention. I brought my naked Pwnagotchi to the airport for ACS CTF and I got questioned during baggage check ;(. I used the linked case files for my case. You can use any open source classic pwnagotchi case and print it yourself.

Notice: In this guide, I am writing about what works for me on November 2023. I am in no way responsible if this guide does not work for you.

<br/>

## Step 1: Flashing the OS

Along several months, I tried different versions and modifications of the pwnagotchi linux-based operating system only to find the 1.5.5 Fix to works. You can find the disk image I used <a href="https://github.com/wpa-2/pwnagotchi/releases">here.</a>

If your laptop/pc has a micro SD card reader installed, plug the micro SD card in. If not, an external micro SD card reader would probably work as it worked out for me. 

Open Balena Etcher, select your SD card and the disk image to start flashing:


<center><img src="/balenaetcher.png" alt="Balena Etcher flashing" width="100%" height="100%"><br/></center>

After the flashing and verification are done, windows might intrude to notify you about the unsupported disk format on the new SD card. Do not click re-format and continue with the next step.

### Step 2: Basic configuration

Before we insert the micro SD card into the raspberry pi, we can do some basic configuration to our Pwnagotchi before its first launch. With your SD card plugged into your computer, enter the SD card (which should now be a boot drive) and make a new file named "config.toml":

<center><img src="/configtoml.png" alt="config.toml" width="100%" height="100%"><br/></center>

Inside config.toml, copy and paste the default initial configuration:


```
main.name = "pwnagotchi"
main.lang = "en"
main.whitelist = [
  "EXAMPLE_NETWORK",
  "ANOTHER_EXAMPLE_NETWORK",
  "fo:od:ba:be:fo:od",
  "fo:od:ba"
]

main.plugins.grid.enabled = true
main.plugins.grid.report = true
main.plugins.grid.exclude = [
  "YourHomeNetworkHere"
]

ui.display.enabled = true
ui.display.type = "waveshare_3"
ui.display.color = "black"
```
The above was taken from the official Pwnagotchi websites's configuration page. However, I have changed ui.display.type to waveshare_3. This gives support to the waveshare V4 screens that are available for purchase today.

Here, you can change the name of your pwnagotchi under "main.name". It is also recomended that you insert the SSIDs or BSSIDs of your home's network and any other networks whos packets you don't want to capture under "main.whitelist".

Although the official Pwnagotchi website may be outdated, a most of the configuration stuff written on the page is probably the same on all Pwnagotchi disk images. Feel free to take a look at the official website <a href="https://pwnagotchi.ai/">here</a> for more configuration options.

### Step 3: First Boot

Before we boot, we have to connect the e-ink display to the raspberry pi. Line up the header pins of the raspberry pi against the receiving end of the e-ink display and push them down until they achieve a snug fit.

