---
title: DUCTF 2023 - Grades
date: 2023-09-03 02:00:00 -0500
categories: [DUCTF 2023]
tags: [DUCTF 2023, CTF]
img_path: /assets/img/DUCTF23/
image: DUCTF23Home2.png
---

## Grades_Grades_Grades

Grades_Grades_Grades is a web CTF challenge for Down Under CTF 2023. Challenge provides a student sign-up page, but flag is only accessible as a more privileged account.

![Grades Problem](GradesProblem.png)

![Grades Default Page](GradesWebDefault.png)

![Grades Signup](GradesWebSignup.png)

Web site is straightforward homepage and sign-up page. Nothing useful yet.

![Grades Tree Files](GradesTreeFiles.png)

In the provided source code there are several files that could be helpful. I primary reviewed the auth.py file.

![Grades Auth Check](GradesAuthCheck.png)

Here, we see 2 references to “is_teacher”. Seems like that is the checked property for access.

![Grades Add Options](GradesBurpAddOption.png)

Grabbing and reviewing the post request from the signup page with Burp Suite, it only adds “stu_num”, “stu_email” and “password” to the account. Adding the “&is_teacher=anything” property manually does add that property to the account. 

(Side note: Originally I used &is_teacher=True. It is only a boolean check in the code, anything besides False or NULL should work and make is_teacher True)

![Grades Flag](GradesFlag.png)

After signing up, the site drops you into your account. With this extra “Grading Tool” page, which contains the flag.

This was a fun web challenge. Wasn’t expecting to just add an additional property and have access. Important to check even the simpler options in ctf challenges.

## Sources:

- [https://play.duc.tf/](https://play.duc.tf/)
