---
title: Drifting Blues 2 - Writeup
date: 2023-02-18 01:00:00 -0500
categories: [Vulnhub, Drifiting Blues]
tags: [Vulnhub, CTF]
img_path: /assets/img/DriftingBlues2/
image: 00Thumbnail.png
---

## Initial Access

### Nmap

To start exploring this machine, I’ll run a standard default Nmap scan with scripts and version detection.

![Nmap Scan](0NmapScan.png)

Nmap returned open services on ports 21,22 and 80. Port 22 is great, likely how we’ll get into the machine at some point, but first we’ll start in the ftp access and that secret.jpg image. Then we’ll move onto the web access.

### Secret Image

![FTP Terminal Access](01FTPFile.png)

For anonymous access, the prompt walks you through, you need username anonymous, and then the password can be something like anonymous@domain.com .  Worked on this machine, then we have ftp access to this one file.  A sectret.jpg.

![Secret singer Photo](02Secretdotjpg.png)

Nothing too unusual with this photo. No obvious usernames or codes in the pixels.

![Exif Photo Details](03SecretdotjpgExfil.png)

Running this image through exiftool to check the meta data, nothing stood out in there either.  This is likely a red herring. 

### Web Layout

To start investigating the port 80 access, we’ll start with Dirbuster to get a layout of the directories available.

![Dirbuster Results](04DirbusterResults.png)

![Dirbuster Scanning](05DirbusterScanning.png)

Dirbuster does let us know that the base url has a site and the wordpress directory after is accessible. Let’s start with http://10.10.10.101/  (or your url equivilant).

![Fake Homepage](06Homepage.png)

Nothing on the “/” site. Let’s head to the “/blog” site.

![Blog Site](07PageBlog2.png)

Looks like there’s more here.  Likely the basic formatting is the linking of the css page being off.  We can see from a link, that this site is supposed to be “driftingblues.box”. We can add that to out hosts file, and see if it formats better.

![Hosts File Edit](08Hosts.png)

![CSS Loaded Blog](08BottomPageBlog.png)

It does return a better formatted site after that.  If the layout from dirbuster of all the wp pages weren’t enough proof of the site’s cms. At the bottom of the site it also says it’s powered by Wordpress. 

### WPScan

Being a wordpress site, we can use a tool called WPScan.  Great for finding wordpress vulnerabilities and with additional options, aggressively try usernames and passwords.

![WPScan Start Scan](09WPScanStart.png)

![WPScan Results Password](10WPScanPassword.png)

And only after a few minutes, we have a hit with albert:scotland1 .  We can try that on the “/blog/wp-admin” page.

![Wordpress Login](11WPLogin.png)

And it works, we now have access to the Wordpress CMS.

### WordPress PHP Shell

If there was a way to drop code to the site to get access or a console of some kind, that would be helpful. Luckily Albert has permissions to edit themes, which contain php pages.

![PHP Theme Edit](12PhpThemePage.png)

If you search for a PHP reverse shell, your likely to get pentestmonkey’s https://github.com/pentestmonkey/php-reverse-shell , which is what I used here in the footer.php.

![Netcat Connection](13NetcatReverse.png)

Running netcat on our attacking machine and visiting the site with malicious php code, should enable our connection.

### RSA Key

![Initial Access](14InitialAccess.png)

![Private Key](15CatPrivateKey.png)

After the connection, we have minimal www-data level access. Not too much we can do at first, but the user’s private key is accessible.  Copying that to our machine should allow use to log in as freddie.

### User Flag

![User SSH connection](16UserSSHaccess.png)

Verifying we set the file to the correct permission level on our attacking machine, we should then be able to log in as freddie and have access to the first flag.

## Escalating Access

### Linpeas

To start looking to how to escalate access, I’ll make a temp folder in “/tmp/” and run python’s httpserver on my attacking machine to serve files.

![File Upload](17UploadFiles.png)

I’ll upload linpeas.sh and pspy64 to the victim’s machine. (pspy64 was not needed for this machine) And then run linpeas with some extra options to save the output and view with less later.

![Linpeas CVEs](18CVEsLinpeas.png)

Reviewing the linpeas output, it does recommend these exploits. CVE-2021-3156 is the one we’ll be using this “Heap-based buffer overflow in Sudo” exploit.  Downloading the file from the provided url, and uploading it to the victims machine.

### Root Flag

![Exploit for Root Flag](19ExploitRootFlag.png)

After running the exploit, our shell has root access and we can view the root flag.

### Cleanup

Cleanup from this box would be to: 

 - Delete your uploaded files to “/tmp/”. 
 - Delete your logs or just all logs from “/var/log”.  
 - Finally would be to revert whichever php file you added the reverse netcat to in the wordpress admin portal back to how it was before you changed it.

## Conclusion

This was another good CTF in the DriftingBlues series.  Vulnerabilities on this machine that lead to a takeover include a weak password on a wordpress account, the RSA private key having wrong permissions configured and being vulnerable to CVE-2021-3156. 

Looking for RSA key pairs could be something useful to search for in future machines. Other than that and the accessible php pages in the wordpress themes, machine was pretty straight forward. Excited to see what’s on the next Drifting Blues machine.

## Sources & Resources


- [https://www.vulnhub.com/entry/driftingblues-2,634/](https://www.vulnhub.com/entry/driftingblues-2,634/)
- [https://github.com/pentestmonkey/php-reverse-shell](https://github.com/pentestmonkey/php-reverse-shell)
