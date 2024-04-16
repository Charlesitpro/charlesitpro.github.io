---
title: ICTF 2023 - Idoriot Revenge
date: 2023-07-28 02:00:00 -0500
categories: [ICTF 2023]
tags: [ICTF 2023, CTF]
img_path: /assets/img/ICTF23/
image: ICTF23Home.png
---

## Idoriot Revenge


Idoriot Revenge is an easy web based challenge for ICTF2023. This ctf also had an Idoriot challenge before this. That solution was just an url traverse to the /flag.txt, this one was more fun.

The problem starts with only an url.

![Idoriot Revenge Problem](IdoriotRevenge.png)

Login page is pretty basic. As well as a registration page link.

![Idoriot Revenge Login](IdoriotRevengePage1.png)

This page does state that the database is wiped every 30 minutes. Could wait until refresh and try to register a certain user like admin first. But, I started with a test account username and password.

![Idoriot Revenge Registration](IdoriotRevengeRegistration.png)

Once logged in the page is filled is filled with php code. Looks like the requirements for the flag are a userid of php and a username of admin. Userid is simple in the url can be changed.

For the admin login, I tried admin’1=1-- as the username when registering. Since this is a sqlite database, I started to try sql injection usernames. This one worked.

![Idoriot Revenge Source](IdoriotRevengeZoomedProblem.png)

After logging in as admin or admin’1=1--, I changed the user_id to php and got a flag.

![Idoriot Revenge Solved](IdoriotRevengeSolved.png)

This was a good beginner challenge. I like that you can use sql injection for the admin login. I’m sure there are other ways to login as admin, but this one worked for me.

## Sources:

- [https://2023.imaginaryctf.org/](https://2023.imaginaryctf.org/)