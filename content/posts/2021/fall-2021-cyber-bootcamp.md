---
title: "Cybersecurity Bootcamp Fall 2021"
date: "2021-09-08T22:30:05.000Z"
tags: ["recap"]
cover:
  image: "/images/2021/09/cybersecurity-bootcamp-1.png"
---


The cybersecurity bootcamp consists of two sessions where we cover a very high-level overview of the cybersecurity world. In the first session, we cover **blue-teaming** , the defensive side of cybersecurity. In the second session, we cover **red-teaming** , which is the offensive side.

# Defensive Security

Defensive security specialists, or blue teamers, are people that perform analysis on information systems to secure and protect them. They try to identify potential threats, restrict system access to only those that need it, harden systems against outside intruders, analyze information to detect an attack, and then when an incident happens, respond to it quickly.

## Threat Intelligence

Threat intelligence is knowledge that allows defenders to prevent or mitigate cyber attacks and helps to provide context in order to make informed security decisions. Asking questions such as: who is attacking you? and what are their motivations and capabilities? are very important for threat intelligence. One thing to look for in systems are indicators of compromise, or (IOC), which is some piece of evidence that indicates that someone malicious has gotten into the system. There are three main types of threat intelligence:

  * **Strategic Intelligence** : This provides a broad overview of an organization's threat landscape. It is primarily intended for higher-level, less technical people such as executives so they can allocate necessary funds and people for securing the company.
  * **Tactical Intelligence** : This focuses on the immediate future of an organization's security. This type is meant for a more technical audience and typically relies on looking for IOCs obtained from open source or free data feeds.
  * **Operational Intelligence** : This focuses on knowledge about cyber attacks, events, or campaigns. This is also meant for a technical audience and is focused on understanding the capabilities, infrastructure, and tactics, techniques, and procedures of threat actors.

Threat intelligence is very useful because it can be used in incident response to help respond to events faster, provide fast, relevant alerts to a Security Operations Center, and help prioritize patching vulnerabilities based on their risk level.

## Cryptography

Cryptography is the development of secure information and communication techniques derived from mathematical concepts and algorithms. It is used nearly everywhere in information systems, from communication protocols like HTTP or SSH to file transfer protocols like SCP or SFTP. Crypto works by using encryption and decryption. Encryption is the act of taking the data and making it difficult for a third-party to read it using an algorithm known as a **cipher** using a type of secret key. Decryption is simply the opposite of this, taking an unreadable encrypted message and turning it back into the original message. There are two main types of ciphers that are used, symmetric and asymmetric.

  * **Symmetric ciphers** use the same key to encrypt and decrypt messages, with this key being shared between the sender and receiver.
  * **Asymmetric ciphers** use two keys, one for encryption and one for decryption. The encryption key, or public key _is not_ secret and the decryption key, or private key _is_ secret. So anyone can encrypt messages with the public key, but they can only decrypt those messages if they have the correct private key.

One very popular crypto algorithm is AES, of which the most common form is AES256. This is by far the most widely used symmetric encryption algorithm because it is fast, widely used in industry already, and does not have any feasible attacks against it right now. One cipher that is not used too much on its own but it used very commonly in other ciphers is the XOR cipher. This simply takes a key and XORs it with the plaintext, creating a symmetric cipher.

## Network Analysis

Network analysis is the process of monitoring and analyzing network traffic to prevent and identify malicious activity. Some of the goals of network analysis are to identify anomalous behavior and investigate it to see if it is malicious, identify possible weak spots in the network to see if they need to be fixed, and make sure the network is configured and managed properly. Networks are a necessity for any organization and are something that attackers commonly look for vulnerabilities in, so it is important to have good network security.

## System Analysis

System analysis is very similar to network analysis, but instead of monitoring an organization's network, it looks at the actual systems. The goals are similar to network analysis like detecting anomalous behavior and preserving logs for future incident response. System analysis looks at what is happening on each system, analyzing things such as Windows Event logs, running processes, and even just files on the machine. It also involves looking at Windows Domain information such as account modifications, what administrator accounts there are and what they are doing, and policy changes.

## Reverse Engineering/Malware Analysis

Malware analysis is the process of taking apart and analyzing potentially malicious programs, and one large part of that process is reverse engineering. Reverse engineering is the process of taking software apart and analyzing it, either with the original source code, or without it (called binary reverse engineering and it what will be talked about the most this semester). Malware is simply any piece of software or program that does something to harm the user, computer, or network. Malware analysis is the art of dissecting that software to figure out how it works, how to identify it in the future, and how to defeat or eliminate it. There are many, many different kinds of malware, with some of the most common types being viruses, which replicate using a host program, ransomware, which blocks access to a system until a certain sum of money is paid, and trojans, which masquerade as legitimate programs. Additionally, there are two main types of malware analysis.

  * **Static analysis** is the process of analyzing the code or structure of the program to determine its functionality without actually running it. This is done by looking at the ASCII strings in a file or Windows function calls and DLL imports. Then, the program can also be disassembled to look at the assembly code directly using a tool like IDA or Ghidra.
  * **Dynamic analysis** is the process of analyzing the malware by actually running it in a sandboxed environment (NEVER run malware on your host machine). Some examples of things to look at during this step are to see what network connections the malware is trying to make, look at any new processes that were created, and compare the registry before and after running it to see what it changed.

## Digital Forensics

Digital forensics involves the investigation, collection, analysis, and recovery of digital artifacts. Performing proper digital forensics on an organization's systems after an incident is very important, as information gathered can help to build a timeline of the incident to understand how it happened and how to mitigate it in the future. The main principle that digital forensics (as well as physical forensics) operates on is Locard's Exchange Principle. This states that the perpetrator of a crime will always bring something into the crime scene and will always leave with something. The main three parts of digital forensics are network forensics, disk forensics, and memory forensics and since we already touched on network analysis, this will focus on disk and memory forensics.

  * **Disk Forensics** is the process of analyzing an image of an infected system's hard drive. Looking at a disk image can provide a lot of valuable information to a forensic investigation, such as looking at what files were on the computer or what programs were installed. Additionally, disk forensics will also show "hidden" items such as deleted files.
  * **Memory Forensics** is similar to disk forensics but instead of looking at a system's disk image, analysis is done on an image of the device's main memory. Memory forensics allows investigators to see things that are impossible to see on the disk. Some of these items include what processes were running and where they were running, shells that were open on the computer and what commands were run, and even inbound and outbound network connections.

# Offensive Security

Offensive security is the assessment of a system or organization's security posture through the perspective of an adversary. Essentially, it is when people think like the "bad guys" in order to find and report vulnerabilities in an organization's security. Before going further into offensive security, there are a few terms to define.

  * A **vulnerability** is a bug, misconfiguration, or other design flaw that is not _necessarily_ something that an attacker can always put to use.
  * An **exploit** is when a vulnerability can be leveraged for the attacker's gain and defender's loss.
  * Finally, a **threat** is a scenario where an attacker leverages a vulnerability to attack a system.

## Red Teaming and Pentesting

Pentesting is when offensive security experts try to find as many vulnerabilities and configuration issues as possible within the timeframe of an operation. This is not typically about about finding new, "zero-day" vulnerabilities, but is more about looking for known vulnerabilities and creating a proof-of-concept with the ones that are found. This is typically a very "loud" operation (i.e. invasive and easily detectable scans are used). Red teaming however, is a much more targeted approach than pentesting. This is typically not about finding as many vulnerabilities as possible, but is more focused on reaching certain objectives to simulate what an actual threat actor would do. Operations can be as short as a pentest, or can last many years. This type of operation is usually much, much quieter, as red teamers must pick vulnerabilities that will help them reach their goals, but will also keep them from being detected.

## Cyber Kill Chain

The cyber kill chain is a series of steps that follow a cyber attack from the early stages of it to the final data exfiltration. This chain is something that many offensive security experts follow to some degree when they plan and conduct an operation.

### Stage 1: Reconnaissance

Reconnaissance is the act of collecting general information about the target, focusing on assessing targets, tactics, and preparing for an attack. One of the main ways this is done is by using open-source intelligence, or OSINT. OSINT is simply the act of gathering information about a target using publicly available resources such as public websites, social media, Google Dorking, and many more.

### Stage 2: Intrusion

Intrusion uses the information gathered from stage 1 in order to find a way into the network and establish some kind of foothold. There are many ways to go about this, with some common ones listed below.

  * **Port scanning and finding vulnerable services** : This is one of the easiest ways to find potential ways in, however, it can have many downsides. If the wrong approach is taken, these scans can be very loud and alert the target that someone is attempting to find a way in.
  * **Phishing** : This can sometimes be a very good way in, as people are almost always the weakest link when it comes to a secure environment. However, this can also be bad if the organization has good email filtering, or if the employees are well-trained to recognize these emails.
  * **Default creds** : People are lazy, and many times when someone at an organization sets up a new tool or service, they may leave default credentials in place, allowing easy access to the network.

### Stage 3: Exploitation/Persistence

Now that a foothold has been established on the network, a way to stay on that network needs to be put in place, commonly called establishing _persistence_. The connection to the network needs to remain in place even if the system is rebooted, or if they find what user account was used to access the system.

### Stage 4: Privilege Escalation

Now that persistence has been established, the next step is to figure out how to become a more privileged user so more can be done to the system and to allow easier movement around the network. Some common ways of doing this include looking through the system to find plaintext passwords, exploiting sudo rights, manipulating or impersonating tokens, or abusing specific binaries, among many other things.

### Stage 5: Lateral Movement

As a privileged user, now it is much easier to move around the network and get an idea of what it looks like and what is on it. The process of doing this is called lateral movement. In moving around the network, it is valuable to look for other interesting systems to potentially establish some form of persistence to.

### Stage 6: Obfuscation/Anti-Forensics

This stage is focused on keeping an attacker's presence on the network hidden from potential defenders. This could include anything from hijacking a legitimate binary as a persistence mechanism to configuring system logs to ignore an attacker's presence.

### Stage 7: Denial of Service

Once network persistence and control is established, an attacker can start denying users from resources on the network. This could include changing firewall rules to block legitimate IP address, crashing systems, or deleting important resources.

### Stage 8: Exfiltration

The final stage is data exfiltration, or the act of pulling information out of the network. An attacker needs to know exactly what data they want to retrieve, where that data is stored on the network, and how they will pull the data off the network to wherever they want it.

### Session 1 Livestream Recording

### Session 2 Livestream Recording
