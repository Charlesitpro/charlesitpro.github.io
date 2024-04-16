---
title: DUCTF 2023 - Helpless
date: 2023-09-03 01:00:00 -0500
categories: [DUCTF 2023]
tags: [DUCTF 2023, CTF]
img_path: /assets/img/DUCTF23/
image: DUCTF23Home2.png
---

## Helpless

Helpless is a miscellaneous CTF challenge for Down Under CTF 2023. Challenge drops you directly into a python interactive help prompt and directs you to where the flag is located.

![Helpless Problem](HelplessProblem.png)

![Helpless Start](HelplessStart.png)

SSHing the provided machine, does drop us into an interactive python help cli. Exiting the interactive cli also exits the SSH connection. Probably will have to use the python interactive in some way to get the flag.

![Helpless Print help](HelplessPrint.png)

Printing the help page for python “print” works. Doesn’t show any options directly on the bottom. Reminds me of a vimjail challenge from another ctf, where either commands needed to be piped into the initial connection or using less documented features of the cli. Piping in commands via ssh didn’t seem like the appropriate approach. Pressing the “H” key did yield some results..

![Helpless Less Command](HelplessPrintLess.png)

The “H” key drops into a LESS help page. Slightly part of the name of this challenge, likely on the right trail. Scrolling down the Less help page shows more options.

![Helpless Less Change](HelplessPrintLessChangeFile.png)

“:e” lets you examine files. If we have the appropriate permissions for the flag file, that could be the end of this challenge.

![Helpless Less Examine](HelplessPrintLessChangeFileExamine.png)

![Helpless Less Examine Open](HelplessPrintLessChangeFileExamineOpen.png)

And then the flag is revealed. A simple solution to the challenge. Didn’t find this documented too much on the web. The process of finding these commands was fun.

## Source: 

- [https://play.duc.tf/](https://play.duc.tf/)
