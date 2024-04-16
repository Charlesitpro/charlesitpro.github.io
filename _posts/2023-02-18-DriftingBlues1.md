---
title: Drifting Blues 1 - Writeup
date: 2023-02-18 00:00:00 -0500
categories: [Vulnhub, Drifiting Blues]
tags: [Vulnhub, CTF]
img_path: /assets/img/DriftingBlues1/
image: 0Thumbnail.png
---

## Summary

This is a fun and easy level CTF by author: tasiyanci through vulnhub.com. It is rated difficulty easy, which I agree. It does lead you to the next step through each new discovery.

I would recommend this CTF to beginners, before reading this walk through.

## Initial Access

To start exploring this machine, I’ll start with a Nmap and Dirbuster scans.  Dirbuster did not return anything interesting, except for /secret.html that only says to “dig...deeper”.

### Nmap

![Nmap Scan](1NmapScan.png)

However, with the Nmap scan, with default scripts and versions detected, we have an available ssh port and http port open.  The ssh port we’ll come back to later, but that will be the entry point as a user and then to escalate permissions.

### Web Page

![Website Homepage Navagation](0Thumbnail.png)
![Website Homepage Body](3EmailonPage.png)

Investigating the http homepage through port 80, there doesn’t seem to be any functional links or forms to use.  However there are potential usernames (Sheryl and Eric) and url (driftingblues.box) that will be useful later.

### Page Source

![HTML Website Code](4InspectWebpage.png)

Inspecting the page, there is a comment that looks like Base64 encoding. Especially, with the “=” equal sign ending. <!--L25vdGVmb3JraW5nZmlzaC50eHQ=> . You could also have used curl with a grep search of strings for comments starting with “<!--”, curl 10.10.10.102:80 \| grep "<\!--".

![Base64 Decoded](5Base64.png)

Decoding this base 64 string reveals another web page. /noteforkingfish.txt

### Ook! Decode

![Ook. Message Repeat](6Ook!.png)

At first glance, this looks like a code.  With irregular punctuation.  At first I suspected a encrypted morse code, however this is an esoteric operating program language called “Ook!”.

![Ook Decoded](7OokCoverted.png)

Sure enough, this decodes to “my man, i know you are new but you should know how to use host file to reach our secret location. -eric” . Leading us to modify our host file and use vhost enumeration.

### Vhost Enumeration

![Hosts File Edit](8HostsEdit.png)

We can use the website from the email we found on the homepage earlier “driftingblues.box” and see if that returns any results.

![Gobuster Scan](9GobusterScan.png)

Using gobuster and the vhost emueration, we can find test.driftingblues.box with a 200 status.

![Hosts File Edit Again](A0HostsEdit2.png)

After adding that to our hosts file.

### Nikto Search

![Nikito Scan](A1NiktoScan.png)

We could explore this version of the site manually, but using a tool like Nikto is faster. Nikto does find, in the robots.txt file that /ssh_cred.txt is a disallowed search engine site.

![SSH Cred Leak](A2sshCred.png)

Indeed, this does have good information.  Giving us 10 options for passwords, making it easier for password attempts.

### SSH Username/Password Attempts

![Crunch Password List](A3CrunchPasswords.png)

Using crunch, we can quickly have a password list of these possibilities.

![MSF Password Try](A4msfScan.png)

And now, using metasploit, we can enumerate through the 30 combinations with username “db”, “sheryl” and “eric”. “db” was from the “/ssh_cred.txt” page signature and “sheryl” and “eric” were usernames from the homepage.

### User Flag

![User Flag Printout](A5UserFlag.png)

This will gives us initial user access.  With metasploit, a session is already opened with those credentials and we can access the user flag.

## Escalating Access

Now that we have a username and password for SSH, we can log in and run some scans. I like to make a folder in the tmp directory, to keep everything together and for easy clean up. We’ll start with “wget”ing linpeas.sh and pspy64 from our attacking machine using python’s SimpleHttpServer.

**Linpeas stands for a Linux Privilege Escalation Awesome Script and is part of the PEASS-ng group.  And is great script to scan for vulnerabilities and different files that can interesting and does not require root privileges to run.

**Pspy64 is a 64-bit version of the pspy - unprivileged Linux process snooping. Pspy is useful to show linux running process without root permissions.

### Linpeas/Pspy64 Scans

![Linpeas Backup Found](A6LinpeasCron.png)

Linpeas says there may be CVEs, I was not successful with them, but there also is an automate cron job. That we can explore with PSPY64.

![Linpeas Cron Jobs](A6ALinpeasBackup.png)

Also, there are backup files including a back script in var/backups/backup.sh

![PSPY Processes](A6BPspy64Backups.png)

After uploading and executing pspy64 to review processes, we can see backup.sh being called from the shell and also emergency being called with sudo. Backup.sh spells it out, that emergency is supposed to be a back door.

In /tmp there is no emergency file currently. So, we can make one with nano.

### Edit Root Script

![Emergency File Edit](A8EmergencyFile.png)

This file can be almost anything to get root privileges, since it is being ran as root.  You could create another user with root privileges, print the contents of root, or escalate eric to the sudo group.  I found this way of making a bash file, and impersonating the creator group great and cleaner, to get the flag and to remove after.

Chmod u+s is used to create the file executable with the user’s id. Chmod a+x should be used on the emergency file, after it’s been created and edited for the cron job to run it.

![Cron Root Process](A9CronRootBash.png)

Running the pspy64 program again, we can see when emergency is ran with sudo permissions, creating a copy of bash in the temp folder.

### Root Flag

![Root Flag](B1RootBash.png)

Now, running this tmp/bash in privileged mode will let us access the flag.  Afterwards, deleting the /tmp/TmpWork folder and /var/logs should restore and cleanup what we changed.

## Conclusion

This was a good CTF.  There were several steps to get root access, but each step did lead to the next.  I got to find and learn about the pspy64 script and esoteric programming languages, which may be helpful in future CTFs. Excited to see what’s on the next Drifting Blues machine.

## Sources & Resources


- [https://www.vulnhub.com/entry/driftingblues-1,625/](https://www.vulnhub.com/entry/driftingblues-1,625/)
- [https://esolangs.org/wiki/Ook!](https://esolangs.org/wiki/Ook!)
- [https://www.dcode.fr/ook-language](https://www.dcode.fr/ook-language)
- [https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)
- [https://github.com/DominicBreuker/pspy](https://github.com/DominicBreuker/pspy)
