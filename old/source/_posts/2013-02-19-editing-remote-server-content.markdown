---
layout: post
title: "Editing remote server content. Like a boss."
date: 2013-02-19 12:55
comments: true
categories: 
---

So you have a Unix-based host sitting there. It's got some files on it. You
wanna edit those files. Let's pretend you're *not* editing config files though,
because you should be using Git/Puppet/Chef for that. Instead, I'm assuming you're
wanting to maybe make a few adhoc changes somewhere in the filesystem. I'm also
assuming it's no longer 1994 and you don't use FTP for productivity/development 
out of principle.

Enter [sshfs](http://fuse.sourceforge.net/sshfs.html). Briefly, SSHFS is a FUSE
driver that allows you to mount a remote filesystem locally, using SSH as the
transport. The benefits of this should be immediately obvious:

* Instantly secure.
* Ubiquitous support - only requires OpenSSH server on the remote end.
* Easy to setup - in most cases there won't be an iota of configuration required
if you've already got your pubkey on the remote.

Installing sshfs is straightward enough on Ubuntu:

```bash
	(sudo) apt-get install sshfs
```

Mounting a remote location is also easy as pie:

```bash
	mkdir -p /local/mount/point
	sshfs remoteuser@remote.host:/remote/location /local/mount/point
	ls /local/mount/point

	# zomgawd the remote filesystem location lists on your local mount point how does that even oh my god what
```

## Bonus points

So the above is all well and good for most use cases, but there's a caveat. What
if you want to edit files as a specific user on the remote host, but you either
don't have direct ssh access to that user, or it doesn't have a shell (the latter
would be more likely if you were editing system config files, but we already
established you're not doing that)? Turns out this is something that sshfs can
handle, too!

What you can do is override some sshfs settings and escalate your privileges to 
the other user when connecting to the remote end. That way, whenever you make
changes locally, the changes are applied using the correct user on the remote 
end. This avoids permission issues, and also means new files will be created 
with the correct user!

In order for this to work, you'll need to have sudo permissions with a user on
the remote host. Specifically, you'll need:

* privileges that DON'T require a TTY, or a password.
* the path to the `sftp-server` binary on your remote host.

Determining the sftp-server path is up to you, as a hint though, you'll probably
find it in the following locations...

**Ubuntu:**
	/usr/lib/openssh/sftp-server

**CentOS 5:**
	/usr/libexec/openssh/sftp-server

**Others**
	locate sftp-server

Then you'll need to make sure your sudoers file has something like the following:

	# Ensure user "remoteuser" does not require a TTY to run sudo.
	Defaults:remoteuser !requiretty

	# Ensure user "remoteuser" can execute sftp-server without a password.
	remoteuser ALL=(ALL) NOPASSWD: /your/path/to/sftp-server

You can ensure the disabling of `requiretty` works by running the following in
your workstation:

	ssh remoteuser@remote.host "sudo -v"

If you don't get any errors, then you can assume all is peachy.

With that out of the way, you can now execute this on your workstation:

	shfs remoteuser@remote.host:/some/path /local/mount -o sftp_server="/usr/bin/sudo -u otheruser /path/to/sftp-server"

Voila! Now when you make changes to `/local/mount` on your workstation, the 
changes will be made using the `otheruser` on the remote host.

Go forth and securely edit remote filesystems with wild abandon!