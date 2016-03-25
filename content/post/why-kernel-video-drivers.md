+++
date = "2014-10-17T20:20:00+01:00"
title = "Why kernel video drivers?"
image = "images/drm.png"
banner = "images/drm.png"

categories = [ "The Kernel" ]
tags = [ "Video drivers" ]
toc = false
+++

Many people wonder why video drivers are moved to the kernel. The
previous way of doing things was working fine and was supported by all
Unix. Now, they are afraid of switching to those kernel drivers because
they don't understand the reason behind them and have heard about
instability and unequal levels of support between different OS versions
and GPU makers.

I'll try to explain the reasons I know, in the hope you'll better
understand and accept this major change in the way we use video cards
nowadays.

* The **X server was an operating system by itself**: it was able to
  scan the PCI bus to find video devices and it manages the video
  memory. That's why it could work on many incompatible kernels: it
  doesn't use any of its facilities. This approach has obviously many
  major issues, detailed in the following bullets.
* The **kernel and the X server were both managing hardware**. This was
  far from elegant and broke features such as suspend/resume.
* The **X server required root privileges**. That's why it's
  installed with the "setuid” bit set, otherwise a regular
  couldn't start an X session.
* The **performance was terrible** compared to platforms (eg. Microsoft
  Windows) where the video drivers are in the kernel (like any other
  drivers).
* The architecture of X and the tighly integrated drivers made it **hard
  to reuse the code** if one wants to implement an alternative, such as
  Wayland. But that was true for the system console too: it needed to
  drive the video card.
* **GPGPU wasn't possible** without running an X session, because only
  the X server was capable of handling the GPU.
* It **wasn't possible to access the GPU from a virtual machine**, for
  the same reason as above.

Today, the kernel drivers address or will address all of these issues.

Regarding GPGPU using free open-source software on FreeBSD, it's still
a work in progress. A "Hello World” OpenCL program works on my
machine, but more packaging and polishing is needed to have something
working out-of-the-box.

The X server still requires root privileges today on FreeBSD because
we lack the APIs and tools to allow the server to gain access to input
devices in a secure manner (remember, the system console needs the
keyboard too).

About using the GPU from a VM, we are still far from this goal, even on
Linux.
