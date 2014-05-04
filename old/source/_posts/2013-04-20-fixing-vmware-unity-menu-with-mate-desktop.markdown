---
layout: post
title: "Fixing VMware Unity menu with MATE desktop"
date: 2013-04-20 11:03
comments: true
categories:
- Ubuntu
- MATE Desktop
- VMware Workstation
---

If you're using [MATE Desktop](http://mate-desktop.org/) in a virtual machine
with VMware, you might notice that when you open the Unity Applications menu on
your host, you get an empty list.

Luckily, there's an easy fix.

```bash
	cat >> ~/.profile <<MATEFIX
	# Fix VMware Unity mode for MATE.
	XDG_CURRENT_DESKTOP=GNOME
	export XDG_CURRENT_DESKTOP
	MATEFIX
```

Run the above, log out and back in to your desktop, and re-enter VMware Unity.
Ta-da!

The issue is that a VMware tools utility, `/usr/bin/vmware-xdg-detect-de`, does
not recognize MATE (even though MATE is just GNOME2), so by setting the 
environment variable `XDG_CURRENT_DESKTOP` in your .profile, you force VMware
to recognize your desktop as **GNOME**.
