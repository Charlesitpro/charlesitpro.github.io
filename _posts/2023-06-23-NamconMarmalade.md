---
title: Namcon 2023 - Marmalade
date: 2023-06-23 4:00:00 -0500
categories: [Namcon 2023]
tags: [Namcon 2023, CTF]
img_path: /assets/img/CTFNamcon23/
image: CTFNahamConHome.png
---

## Marmalade 5

Marmalade 5 is a medium challenge (started as an easy challenge) for the Nahamcon 2023 CTF by @congon4tor#2334. It’s a web challenge that I found difficult and couldn’t get to work.

![Marmalade Problem](Marmalade1.png)

To start with the site, it’s very plain. It’s let’s you log in as any username you want.

![Marmalade Homepage](MarmaladePage.png)

I tried “ThisIsAUsername” and I did not get the flag. Apparently, the flag is under the admin account.

![Marmalade Homepage Fail](MarmaladePage1.png)

If we enter “admin” as the username, we are greeted with the problem that, admin can’t log in.

![Marmalade Admin](MarmaladePageAdminLogin.png)

Searching our browser, we can the cookie left from logging in. This is a JavascriptWebToken. 

A JWT has 3 parts, the header, payload and signature. All just base64 encoded. The code I have for the username is  eyJhbGciOiJNRDVfSE1BQyJ9.eyJ1c2VybmFtZSI6IlRoaXNJc0FVc2VybmFtZSJ9.YN0Md7deANGPEGm_-Fxtxw .  

![Marmalade Page Token](MarmaladePageToken.png)

eyJhbGciOiJNRDVfSE1BQyJ9 is the header, translates to {"alg":"MD5_HMAC"}
eyJ1c2VybmFtZSI6IlRoaXNJc0FVc2VybmFtZSJ9 the payload translates to {"username":"ThisIsAUsername"}
YN0Md7deANGPEGm_-Fxtxw is the signature made from the first 2 parts and a secret password with an algorithm. 

Likely the algorithm is “MD5_HMAC”. If we put in an incorrectly signed JWT, we get the below “Bad Request” page.

![Marmalade Bad Request](MarmaladePageBadRequestClue.png)

This gives us a hint on the password. We can crunch a password list with [crunch 16 16 -t fsrwjcfszeg@@@@@ -o outputPasswords.txt] and use a for loop to guess at every possiblity. Or, as other writeups point out, you can use John the Ripper for the password.

After getting the password, you would need to fake a JWT signature with the MD5 HMAC algorithm and password and username admin. Then you should have access to the flag.

## Conclusion

This challenge, I understood what had to happen for the flag, however, I could not get python or C# to run how I wanted it to. I did get to learn about JWT and the variety of algorithms for signing JWT.

It was a good problem that forced me to learn new ways of authenticating. I look forward to solving a similar CTF challenge in the future.

## Final CTF Conclusion

Overall, the Nahamcon CTF was very fun. Enjoyed the discord and the exercises. Would have liked more time personally, to look at more challenges. I would recommend Nahamcon CTF to people of low to mid cyber skill level. Not sure on the higher harder challenges, but they looked realistic and extensive from a quick glance.



## Sources:

- [https://ctf.nahamcon.com/](https://ctf.nahamcon.com/)