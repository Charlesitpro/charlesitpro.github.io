---
title: CorCTF 2023 - Force
date: 2023-07-30 01:00:00 -0500
categories: [CorCTF 2023]
tags: [CorCTF 2023, CTF]
img_path: /assets/img/CorCTF23/
image: CorCTF23Home.png
---

## Force

Force is a web CTF challenge for corCTF 2023. Needed to look into Graphql for this one, where it’s used but nothing is stored in there.

![Force Problem](ForceProblem.png)

The webpage for this challenge is just a textbox and submit button. You could use this to crack the flag, but I used mostly the burp suite.

![Force Start](ForceStart.png)

The code for this challenge lays it out nicely. We have a flag that is only accessible as a return value. We need a pin between 1 to 100,000. And we have the mercurius library imported, which is a Graphql library. Will probably need some Graphql language functions.

Furthermore, there is also a restriction of only 10 requests every minute. (corCTF challenges are only up 10 minutes, so we could brute force up to 100 requests before that instance is over, if needed.) 

![Force Web Code](ForceWebCode.png)

To get this flag, we needed to send a lot of requests in a single request. Mutations are disabled, so we can’t add another resolver. Found several sites for other Graphql libraries for batching, but those didn’t work. Thanks to this site ( https://lab.wallarm.com/graphql-batching-attack/ ) we can use serial execution.

![Force Serial Execute](ForceSerialExec.png)

To do this, I created a python file to print all the possibilities to 10 separate files.

Sending all 100,000 combinations to the server was too much. We needed smaller requests.

![Force All Codes](ForceAllPins.png)

![Force Burp](ForceBurp1.png)

With these 10 groups of queries and request loaded into burp, I ran through each one. Using the search in the response and found the flag.

![Force Flag](ForceFlag.png)

This was a good challenge. If it was a different Graphql library or if there were more articles online about serial execution, this would have been easier. But, I had fun throwing lots of options at this until discovering this technique.

## Sources:

- [https://2023.cor.team/](https://2023.cor.team/)
- [https://lab.wallarm.com/graphql-batching-attack/](https://lab.wallarm.com/graphql-batching-attack/)
