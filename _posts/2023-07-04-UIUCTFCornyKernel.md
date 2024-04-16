---
title: UIUCTF 2023 - Corny Kernel
date: 2023-07-04 02:00:00 -0500
categories: [UIUCTF 2023]
tags: [UIUCTF 2023, CTF]
img_path: /assets/img/UIUCTF23/
image: UIUCTF23Home.png
---

## Corny Kernel

Corny Kernel is an easy challenge for the UIUCTF 2023 challenge. It’s a misc challenge great for Linux beginners to learn some commands.

In the challenge, we are given a file and a socat command to connect. And likely have to do something with drivers or a kernel.

![Corny Kernal Problem](CornyKernalProblem.png)

In the pwnymodule.c we see 2 flags, and an init function and exit function. In these functions, there also an alert and an info messages. That’s where our flag will be. 

During review the code, I had to lookup and learn kernel messages. These pr_alert and pr_info functions will become important later.

![Corny Kernel Pwny Module](CornyKernalpwnymodule.png)

Socatting into the challenge does a lot, by cd-ing us into root and setting up a root like environment. 

We are given a gziped pwnymodule.ko.gz . Decompressing that, we are then left with a .ko file. This is a kernel object file. And we can use kernel management commands like insmod to insert the module, lsmod to list active modules and rmmod to remove modules.

Insmod gives a clear flag part as an alert. The other info message flag is hidden at the moment.

![Corny Kernel Setup](CornyKernalSetup1.png)

Until we run dmsg or kmsg. At the bottom is the alert and info message of the flag.

![Corny Kernel Dmesg](CornyKernalDmesg.png)

This was an easy challenge. Anyone who has used linux for sometime have probably loaded their own drivers or custom drivers before. I have not outside of apt install programs. Fun thing to learn some kernal management commands.

## Source: 

- [https://2023.uiuc.tf/](https://2023.uiuc.tf/)