---
layout: post
title: "SSSD: Cannot load configuration database (FIX)"
date: 2013-05-03 01:03
comments: true
categories: 
- ubuntu server
- system administration
- tips
---

If you're trying to configure SSSD and you get an error message in your syslog
that kinda looks like this:

	May  3 00:55:51 www1 sssd: Cannot load configuration database

... Then you just need to make sure your sssd.conf file has a newline at the 
end. Not even kidding.

	echo >> /etc/sssd/sssd.conf	

I had this particular issue on Ubuntu 12.04 Server. Might be specific to that distro,
although I did find [this sssd ticket](https://fedorahosted.org/sssd/ticket/1847)
that seems to indicate it was an upstream issue, but then again it was closed
as invalid. So I dunno. The invalid resolution fixed the issue for me. YMMV.
