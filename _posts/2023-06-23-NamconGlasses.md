---
title: Namcon 2023 - Glasses
date: 2023-06-23 02:00:00 -0500
categories: [Namcon 2023]
tags: [Namcon 2023, CTF]
img_path: /assets/img/CTFNamcon23/
image: CTFNahamConHome.png
---

## Glasses

Glasses is a warm-up challenge for the Nahamcon 2023 CTF by @JohnHammon#6871. It’s web based challenge and great for beginners.

![Glasses Problem](Glasses1.png)

After launching the webpage, we are greeted with a normal looking shipping site. Links do go where or appear to do anything.

![Glasses Homepage](GlassesPage.png)

However, if we right click, we are given a javascript error alert.

![Glasses Not Allowed](GlassesRightClick.png)

If we curl or wget the webpage, we can see the javascript function that is preventing this. Which is only blocking right mouse clicks. Rest of the html looks obfuscated. 

![Glasses HTML from Curl](GlassesCurlScript.png)

This gives us many options, we can disable javascript in the browser. We might be able to use a multiple button mouse or other unique inputs. Or, we can select the dropdown in settings to access developer tools.

![Glasses Inspect HTML](GlassesRClick.png)

Buried in the html does appear to be a flag. After removing the styling, we get most of the flag. Replace the half symbol with curl braces, we have our flag.

![Glasses flag](GlassesRemoveStyle.png)

Another fun warm-up challenge and an easy 50 points. I liked the blocking of wget, curl and right clicking for html access. Made you think of other tools to access this data. Moving on to the next challenge.

## Sources:

- [https://ctf.nahamcon.com/](https://ctf.nahamcon.com/)