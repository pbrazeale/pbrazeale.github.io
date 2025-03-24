+++
tags = ['CompTIA', 'Security+', 'Linux', 'Networking']
title = 'Security+ Study Guide: Ch03 Malicious Code'
date = 2025-03-15T06:34:07+01:00
draft = false
+++

**Malware**:

- ransomware
- worms
- spyware
- viruses
- keyloggers
- rootkits
  - allows attackers to retain access to systems once they've gained a foothold.

## Malware

"The term _malware_ describes a wide range of software that is intentionally designed to cause harm to systems and devices, networks, or users."

##### Exam Note

"you will need to know the distinctive characteristics of each type of malware, and what might help you tell them apart."

### Ransomware

- Takes over the computer, and then demands a ransom.
  - crypto malware is popular one that encrypts the system's data
  - other common variant is blackmailing with data found on the system.
- _Indicators of compromise_ (**IoC**s)
  - _Command and control_ (**C&C**) - connection to known malicious IPs
  - Legitimate tools used unusually
  - Ransom demands
  - Data exfiltration behaviors (large data transfers)
- Best practice to keep a complete data back offsite that won't be cross infected.

### Trojans

- The Iliad Trojan Horse.
- Software that looks legit, but is in fact a system backdoor.
- Indicators of a Trojan:
  - Malware Signatures
  - Command and control system hostnames and IP addresses
  - Data created on target devices
- _Remote Access Trojans_ (**RAT**s)
  - provide attackers with remote access
    - Sometimes using legitimate tools in malicious ways
- _Endpoint Detection and Response_ (**EDR**)

##### Bots, Botnets, and Command and Control

"These groups of systems that are under central command are called botnets, and individual systems are called bots."

### Worms

- Worms spread themselves
- Worms also self install

##### Stuxnet: Nation-State-Level Worm Attacks

"The 2010 Stuxnet attack is generally recognized as the first implementation of a worm as a cyber weapon."

- "firewalls and network-level controls remain one of the best ways to mitigate worm attacks."

- Raspberry Robin, example of modern worm
  - Common IoCs:
    - Known malicious files
    - Downloads of additional components from remote systems
    - C&C contact to remote systems
    - Malicious behaviors using system commands for injection and other activities, including use of `cmd.exe`, `msiexec.exe`, etc...
    - Hands-on-keyboard attacker activity
- "Patching and configuring services to limit attack surfaces is also a best practice for preventing worms."

### Spyware

- malware designed for reconnaissance
- Similar behavior to above types
- "Since spyware is generally perceived as less of a threat than many types of malware, it is commonly categorized separately and may require specific configuration to identify and remove it."

### Bloatware

- Software that comes prepackaged with a device/system.
  - Not usually intentionally malicious, but creates an attack surface all the same.
  - Also known to use up system resources with no gain for the user.

##### Exam Note

"The Security+ exam outline calls out spyware and bloatware, but they can sometimes be difficult to tell apart since manufacturers who install bloatware often have call-home functionality built into the bloatware."

### Viruses

- "Computer viruses are malicious programs that self-copy and self-replicate once they are activated."
- _Trigger_ what starts it
- _Payload_ what it does
- Types:
  - Memory-resident viruses, which remain in memory while the system of the device is running.
  - Non-memory-resident viruses, which execute, spread, and then shut down.
  - Boot sector viruses, which reside inside the boot sector of a drive or storage media.
  - Macro viruses, which use macros or code inside word processing software or other tools to spread.
  - Email viruses that spread via email either as email attachments or as part of the email itself using flaws inside email clients.
- _Intrusion Prevention Systems_ (**IPS**s)

##### NOTE

"many organizations have a standard practice of wiping the drive of an infected machine and restoring it from a known good backup or reinstalling/reimaging it."

### Keyloggers

- capture keystrokes from the keyboard
  - capture data from the kernel, via APIs or scripts, or directly from memory
- use of multifactor authentication can help limit the impact of a keylogger

##### NOTE

"Hardware keyloggers are also available and inexpensive."

### Logic Bombs

"_Logic bombs_, unlike the other types of malware described here, are not independent malicious programs. Instead, they are functions or code placed inside other programs that will activate when set conditions are met."

### Rootkits

"_Rootkits_ are malware that is specifically designed to allow attackers to access a system through a backdoor. Many modern rootkits also include capabilities that work to conceal the rootkit from detection through any of a variety of techniques, ranging from hooking filesystem drivers to ensure that users cannot see the rootkit files to infecting startup code in the Master Boot Record (MBR) of a disk, allowing attacks against full-disk encryption systems."

- Some are rootkits are intentional:
  - DRM
  - Anti-cheat software
- Secure boot can help protect against persistent rootkits
- Uninstall hard drive and look at it with another machine
  - Since the OS is dormant, the tool may be revealed.

## Review Questions (15/20) 75%

### Correct

3, 4, 5, 6, 7, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19

### Incorrect

1, 2, 8, 9, 20

- 1, didn't consider a code review process would be needed since the threat was internal. It's obvious now though that the logic would likely be too novel to be detected.
- 2, I second guessed myself. Need to trust my initial instinct.
- 8, clearly overthought this one. Partially recalling [Fancy Bear Goes Phishing](https://www.goodreads.com/book/show/62039276-fancy-bear-goes-phishing) and the Bulgarian "Dark Avenger"
- 9, didn't consider D because I selected B instantly. _Need to read all answers first even when single choice_
- 20, Made assumptions about the question leading toward Trojan, but upon rereading it's clearly Virus.

Waited two days between reading the chapter and testing. Based on the performance, I'm leaning toward needing to review the entire book a second time before testing. _I'm considering if I should have bought [CompTIA Security+ Practice Tests: Exam SY0-701](https://www.amazon.com/CompTIA-Security-Practice-Tests-SY0-701/dp/1394211384) to practice further._
