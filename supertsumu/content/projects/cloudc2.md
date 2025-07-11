---
title: "CloudC2"
date: 2022-12-14T11:45:01+08:00
---

[Home](/)

<h1 style="line-height: 1.0;">How to make a command-and-control (C2) server on the cloud</h1>
<br/>

<center><img src="/cloudc2logo.png" alt="hak5 rubber ducky" width="70%" height="70%"><br/></center>

A command-and-control server (C2) is a server where hackers control their victim’s compromised computers via bind/reverse shells. They can come in the form of a simple netcat instance or fully developed frameworks that feature exploitation scripts such as Meterpreter and PowerSploit.

In this article, I will be demonstrating how I hosted my C2 server on the cloud and its capabilities using the Linode cloud hosting service.
<br/><br/><br/>
# Why host on the cloud?


## Risk of having publicly open ports.

To be able to compromise machines in other private networks, we must get the victim’s machine to connect to our machine that has service that waits for a connection. In order for the machines to connect, our attacker machine must be public facing (having a public IP address). This can be done on a normal home network via port forwarding. However,not only this is hard to set up, it puts the devices in your internal network at risk such as your personal computers, smartphones and IOT devices. This is because if other attackers manage to compromise your C2 server hosted using your home wifi, they will be able to communicate with other devices connected to your home wifi and also potentially gain access to them too.

With a C2 server that is hosted on the cloud, attackers are not able to move laterally to other devices since cloud providers will give us a private subnet consisting of only the C2 server, so there will be no other targets for attackers to compromise.

## Convenience of SSH

Since our C2 server is public facing, our cloud providers will often set up SSH services so that we can control our C2 server from our devices. This means that we can hack from any device that supports a SSH client such as a laptop or even Android phone!

<center><img src="/C2phone.jpg" alt="hak5 rubber ducky" width="60%" height="60%"><br/>My C2 server on Android using the Termius SSH client.</center>

<h1 style="line-height: 1.0;">Creating a cloud instance with Linode</h1>
<br/>

Any cloud hosting service could work but I will be working with Linode. You can sign up for an account here. At the time of my writting, Linode is offering 100$ worth of credit for 2 months so it is worth trying this mini project with the free trial.

After signing up and verifying your email and payment information etc, head to the Linode Manager and make a cloud instance by clicking “Create Linode”.

<center><img src="/createlinode.png" alt="hak5 rubber ducky" width="100%" height="100%"><br/></center>

Then, you want to choose a Linux distribution, your region, your linode plan, linode label and a root password. Your chosen region will affect your connection to the server so pick the region closest to you. For the linode plan, I chose the dedicated CPU plan with 4GB of RAM, 2 CPUs and 80GBs of storage. Rapid7 recommends at least 4 gigabytes of RAM to run Metasploit as stated in their [system requirements](https://www.rapid7.com/products/metasploit/system-requirements/).

You might want to consider picking a Linux Distribution other than Kali Linux to hide suspicion but I will be using Kali Linux as it is easier to install Metasploit on the machine. If you decide to use another Linux Distribution, you will have to download Metasploit from their Github page and build it from source or add the Kali Linux repository to your list of repositories before installing with your chosen installer.

Once you have made your Linode, give it a while for it to boot and log into it via SSH from your terminal using:

```bash
ssh root@[IP address of you Linode]
```

At this point, you have successfully created you cloud C2 server. You can start testing it by starting a tcp reverse shell listener using netcat or any other C2 framework such as Metasploit’s exploit/multi/handler. This should work for any device on any network provided you set the LHOST option to your C2 server’s public IP address.

Paired with my DIY USB rubber ducky which you can find here, I am able to get a reverse shell on a computer given a couple seconds of physical access and control it from my cloud C2 server on my smartphone. Due to how quick and easy it is to compromise a machine and control it with a computer disguised as a smartphone on-site, this combo proves to be a great tool when practicing solo red-teaming.

Thanks for reading. If you have any questions about my mini project please contact me on discord at SuperTsumu#9404