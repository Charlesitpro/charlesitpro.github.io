---
title: UIUCTF 2023 - First Class Mail
date: 2023-07-04 01:00:00 -0500
categories: [UIUCTF 2023]
tags: [UIUCTF 2023, CTF]
img_path: /assets/img/UIUCTF23/
image: UIUCTF23Home.png
---

## First class mail

First Class Mail is an easy challenge for the UIUCTF 2023 challenge. It’s an OSINT challenge that I think has an interesting solution. There were several OSINT challenges, this one I learned something new.

The only file provided is a photo, and the challenge is to obtain the zipcode of where this photo was taken.

![First Class Mail Problem](PostnetDecodeProblem.png)

Downloading the photo and reviewing the photo doesn’t show anything too obvious. No specific enough regional products or buildings. The meta data does show latitude/longitude, but as the challenge says, that’s not the correct place.

![First Class Image](PostnetDecodeImage.png)

In the photo, among the various products is a letter’s bottom right code. It took some googling, but this is the POSTNET code. This code does translate to the zip code.

![Letter Codes](USPSFIMLocation.png)

On the wiki there is a guide on how to decode these. [https://en.wikipedia.org/wiki/POSTNET](https://en.wikipedia.org/wiki/POSTNET) . You can also use the dcode.fr site to decode this for you using 1s and 0s for tall and short lines. [https://www.dcode.fr/barcode-postnet](https://www.dcode.fr/barcode-postnet)

![Barcode Postnet Decode](PostnetDecode.png)

Simple and straight forward challenge. Looked at this photo and tried multiple ways before discovering postnet codes. Overall, fun challenge, that if you knew envelope layouts, is a quick 50 points. If you didn’t, fun thing to learn that I’m sure other CTFs may use as well.

## Sources & Resources:

- [https://en.wikipedia.org/wiki/Facing_Identification_Mark](https://en.wikipedia.org/wiki/Facing_Identification_Mark)

- [https://en.wikipedia.org/wiki/POSTNET](https://en.wikipedia.org/wiki/POSTNET)

- [https://www.dcode.fr/barcode-postnet](https://www.dcode.fr/barcode-postnet)

- [https://2023.uiuc.tf/](https://2023.uiuc.tf/)