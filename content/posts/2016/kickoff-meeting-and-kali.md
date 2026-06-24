---
title: "Kickoff Meeting And Kali"
date: "2016-01-25T00:00:00.000Z"
tags: ["ctf", "kali", "recap"]
---


In the first AUCTF meeting we went over the basics of what CTFs are, and then talked about the major suite of tools we use for competitions: Kali Linux.

# What’s a CTF?

Cyber Security is one of the fastest growing career fields right now, but getting practice hacking things and figuring out new skills will lead to legal trouble if you do things you’re not supposed to, and get tedious due to the lack of competitive space. This is where Security Capture the Flags (CTFs) come in.

CTFs are a Jeopardy-style competition where teams compete to find ‘flags’ by solving problems in a number of security related categories that can range from something as simple as nerd-culture [trivia](http://d.ibtimes.co.uk/en/full/1415646/hack-planet-2014-year-hackers-took-control.png?w=736) to cryptography to binary exploitation and reverse engineering to social engineering and OpSec.

We use a number of sites in order to practice for competitions. The best site for writeups and upcoming CTFs is [ctftime](https://ctftime.org). Some of the best legal areas to practice are things called wargames (always active ctfs) which can be found at sites like [Hack This Site](https://www.hackthissite.org/), [Over The Wire](http://overthewire.org/wargames/), and [PicoCTF](https://picoctf.com/problems).

* * *

# Kali Linux

Kali is an operating system that comes with a bunch of penetration testing tools built in, based on its successor ‘BackTrack’; bootable off a flash drive or in a Virtual Machine and is one of the best things available to get started in hacking and CTFs. An iso to build for VMs is readily availabe on [Offensive Security’s](https://www.offensive-security.com/kali-linux-vmware-virtualbox-image-download/) website.

Some of the most used tools include:

Web Applications | Passwords | Reversing | Forensics | Networks/Wireless  
---|---|---|---|---  
BurpSuite | John the Ripper | OllyDbg | BinWalk | Wireshark  
OWASP-Zap | Ophrack | Radare2 | Foremost | Aircrack-ng  
HTTrack | Hashcat | IDA Pro | Scalpel | nmap  
SQLmap | Medusa | Dex2Jar | MagicRescue |    
RainbowCrack | APKTool | Volatility |   |    
  
* * *

We’ll go over most of these tools in depth over the semester.
