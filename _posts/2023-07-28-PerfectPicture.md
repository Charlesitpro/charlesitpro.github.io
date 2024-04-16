---
title: ICTF 2023 - Perfect Picture
date: 2023-07-28 01:00:00 -0500
categories: [ICTF 2023]
tags: [ICTF 2023, CTF]
img_path: /assets/img/ICTF23/
image: ICTF23Home.png
---

## Perfect Picture

Perfect Picture was a challenge in ICTF2023. There were interesting issues I found a long the way to get the flag. It was a fun challenge.

To start, this challenge has an url and a downloaded zip file. I’ll download and unzipped the file for later and looked at the url now.

![Perfect Picture Problem](PerfectPicture.png)

The url leads to a file uploader site. Nothing seems to be too interesting yet. If the file is displayed in some way after uploading, there could be a backdoor we could make.

![Perfect Picture Page](PerfectPicturePage.png)

However, upon uploading anything, we get a decline message.

![Perfect Picture Wrong Page](PerfectPictureWrongPage.png)

Looking at the downloaded file, the main sections we are interested in, are the requirements. Looks like an image of specific dimensions, specific pixel colors and specific meta data are needed.

![Perfect Picture Req](PerfectPictureRequirements.png)

While trying to reverse this, it took me sometime to find out that a image.convert function was needed for the 4 valued color. There are a lot of examples online of 3 value color set pixels, but not these RGBA pixels.

![Perfect Picture Pixel Check](PerfectPicturePixelCheck.png)

The meta data from app.py said PNG:Title and others starting with “PNG:”. The library in my python code didn’t set these like this. I set them manually outside of my pixel setting and checking code. That seemed to work and pass my checking script.

Another weird issue with this, would be after I checked it through my script and it didn’t get any errors, if I ran it again, I would then give errors. Something was opening the file and messing with the metadata or not saving all of it correctly. Luckily, I only this file once and could make it and send it without checking it first.

![Perfect Picture Solve Check](PerfectPictureSolveCheck.png)

Uploading this file with the pixels set and metadata set. The flag is provided.

![Perfect Picture Solved](PerfectPictureSolved.png)

This was a good challenge. Found odd issues with meta data and pixel colors. It was fun to debug those and craft a file for this flag.

## Sources:

- [https://2023.imaginaryctf.org/](https://2023.imaginaryctf.org/)