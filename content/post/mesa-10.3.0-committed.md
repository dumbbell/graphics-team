+++
date = "2014-10-17T20:10:00+01:00"
title = "Mesa 10.3.0 committed!"
image = "mesa.png"

categories = [ "The Ports tree" ]
tags = [ "Mesa", "OpenCL", "Wayland" ]
+++

Today, [Koop Mast committed an update to the Mesa
ports](https://svnweb.freebsd.org/ports?view=revision&revision=371035)
to have both 9.1.7 and 10.3.0 available.

## What's new?

Mesa 10.3 brings **major improvements in stability and performance**,
especially for Radeon owners, compared to Mesa 9.1. For instance, it
fixes many of the GPU lockups you may see.

With Mesa 10.3.0 comes a new port as well: `graphics/gbm`. This buffer
management library is used by other components inside and outside Mesa,
such as:

* GLAMOR, the 2D acceleration API based on OpenGL, used by at least newer Radeon cards;
* Weston, the reference compositor from the Wayland project;
* Clover, the OpenCL library in Mesa.

Beside those components, the X.Org server 1.15 requires Mesa 9.2+ too.

## Only for FreeBSD 10.1+

We still need Mesa 9.1.7 because our Intel i915 driver in FreeBSD 9.x
and FreeBSD 10.0 lacks a feature called
"[HW context](https://bwidawsk.net/blog/index.php/2013/01/i915-hardware-contexts-and-some-bits-about-batchbuffers/)".
This feature allows the switch between multiple OpenGL contexts without
having to resend them to the card after each switch. Mesa 9.2 and later
versions require this. That's why Mesa 10.3.0 can't be used on FreeBSD
9.x or 10.0.

However, FreeBSD 10.1 and 11-CURRENT
[have this feature](https://svnweb.freebsd.org/base?view=revision&revision=271705).
In this case, Mesa 10.3.0 will be picked automatically.
