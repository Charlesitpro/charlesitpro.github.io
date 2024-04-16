---
title: UIUCTF 2023 - At Home
date: 2023-07-04 03:00:00 -0500
categories: [UIUCTF 2023]
tags: [UIUCTF 2023, CTF]
img_path: /assets/img/UIUCTF23/
image: UIUCTF23Home.png
---

## At Home - almost

At Home is an easy crypto challenge for the UIUCTF2023. It’s a challenge I spent some time on, but did not get the flag.

This challenge provides a text file and python file. The text file has your e, n, and c variables for the python file.

![At Home Problem](AtHomeProblem.png)

Inside the chal.py file, we see where is, in the flag variable as a binary. Also a lot of skip-able lines until the c= equation with  flag.

![At Home Challenge](AtHomeChal.png)

The approach I tried was a type of bruteforce, for getting the flag in bytes. Started with a different while loop looking for flag size, by multiplying by 10, until the while loop ended. 

Once I had the size, I could then narrow down the value from checking large ballpark numbers to then narrowing it down to more fine grain numbers. Starting a new counter for each digit from left to right.

Finally in the code, printing out what it has found and converting back to ascii.

![At Home Close](AtHomeCloseSolution.png)

Running this script, the c value I get from brute-forcing is the same as the challenge's c value. Although the flag value doesn’t seem right. Unsure if I decoded this wrong or if there is another half of flag in the this challenge. Not sure. Haven’t seen anyone else post a writeup for this challenge yet. Would like to see what step I’ve missed.

![At Home Solution Output](AtHomeCloseSolOutput.png)

This was an fun challenge. Haven’t done many cryto challenges yet. There may have been an algorithm to reverse the initial flag encoding program. But, I like that there is a way to get the answer with quick brute-forcing that doesn’t take hours or days.

## Source: 

- [https://2023.uiuc.tf/](https://2023.uiuc.tf/)
