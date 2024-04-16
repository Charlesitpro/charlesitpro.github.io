---
title: Namcon 2023 - Fast Hands
date: 2023-06-23 01:00:00 -0500
categories: [Namcon 2023]
tags: [Namcon 2023, CTF]
img_path: /assets/img/CTFNamcon23/
image: CTFNahamConHome.png
---

## Fast Hands

Fast Hands is a warm-up challenge for the Nahamcon 2023 CTF by @JohnHammon#6871. It’s web based challenge and great for beginners.

![Fast Hands Challenge](FastHands1.png)

After launching the webpage, there only appears to be a blue “Capture the Flag” button.

![Fast Hands Homepage](FastHandsPage.png)

Clicking on the button quickly opens and closes a pop up window.

![Fast Hands Pop up](FastHandsPage1.png)

Investigating the html, you can see that the button redirects to /capture_the_flag.html .

![Fast Hands HTML](FastHandsPageInspect.png)

Going there be editing the browser’s url, brings up a green flag button.

![Fast Hands Almost Flag](FastHandsPageNext.png)

And investigating this html page, you can find the flag in a none displayed span element.

![Fast Hands Flag](FastHandsPageNexFlag.png)

Nice way to warm-up with an easy 50 points. I enjoyed the pop-up page element of this challenge. Moving on to the next challenge.

## Sources:

- [https://ctf.nahamcon.com/](https://ctf.nahamcon.com/)
