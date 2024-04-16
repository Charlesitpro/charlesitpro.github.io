---
title: Namcon 2023 - Open Sesame
date: 2023-06-23 03:00:00 -0500
categories: [Namcon 2023]
tags: [Namcon 2023, CTF]
img_path: /assets/img/CTFNamcon23/
image: CTFNahamConHome.png
---

## Open Sesame

Open Sesame is an easy challenge for the Nahamcon 2023 CTF by @JohnHammon#6871. It’s a binary exploitation challenage and great for beginners.

![Open Sesame Problem](OpenSesame1.png)

We don’t need to launch the challenge to start, the 2 files to download is the puzzle and the netcat is for the flag.

Looking at the code in open_sesame.c, we can see the password at the top. If we use that now, by itself, nothing would happen. Later in the code shows that. 

We are using strncmp(). That’s not the best idea. It only checks the first part of a string and we also have a max the string size for the inputPass at 256 characters. As well as a pointer passed to check a password.

After seeing these functions, likely going to be an overflow type exploit.

![Open Sesame Code](OpenSesameCode.png)

Sure enough, if we scroll down, we can see the scanf() for input. An impassable if statement and our flag function.

![Open Sesame Function](OpenSesameCodeFunction.png)

Since we have the password and the max characters for the input. Let’s try putting in too many characters.

![Open Sesame Code Proof](OpenSesameCodeProofConcept.png)

Sure enough that does it. Checking the netcat connection, gives us the flag.

![Open Sesame Code Proof Flag](OpenSesameCodeProofConceptFlag.png)

This challenge was a nice easy coding 50 points. If you didn’t know how to read code, this could be difficult. Few functions and structures to learn.  Overall, fun problem. Moving to my final CTF challenge I attempted.

## Sources:

- [https://ctf.nahamcon.com/](https://ctf.nahamcon.com/)