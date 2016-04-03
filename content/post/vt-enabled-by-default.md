+++
title = "vt(4) enabled by default"
date = "2014-10-19T20:10:00+01:00"
author = "Jean-Sébastien Pédron"

featured = "vt100.jpg"
featuredpath = "/images"

categories = [ "The Kernel" ]
tags = [ "Console" ]
toc = false
+++

vt(4), the new console driver, is [enabled out-of-the-box in FreeBSD
11-CURRENT](/https://svnweb.freebsd.org/base?view=revision&revision=274085)
(the development branch of FreeBSD) as of today!

For those who don't know it yet, vt(4) brings important features:

* It **supports Unicode** and double-width characters. It finally allows
  to use an UTF-8 locale.
* It **integrates with the new kernel video drivers**. That means that
  you can switch from an X session to the console and back. syscons(4)
  was never taught about the KMS drivers, and this was a major
  regression for users because the screen was blank when vt-switching or
  terminating the X server.

<!--more-->

vt(4) has still some issues. Furthermore, it lacks some features
compared to syscons(4). Known issues are [listed in the
wiki](/https://wiki.freebsd.org/Newcons#Known_Issues) and/or
[recorded in Bugzilla using the "vt” keyword](/https://bugs.freebsd.org/bugzilla/buglist.cgi?keywords=vt&list_id=28354&resolution=---).

Refer to the associated `UPDATING` entry to get information about updated
console settings in `/etc/rc.conf` or how to select syscons(4).
