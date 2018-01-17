---
number: 5
title: SELinux Logging
description: Learn how SELinux reports denials
attribution_url: https://wiki.gentoo.org/wiki/SELinux/Tutorials/Where_to_find_SELinux_permission_denial_details
next_tutorials: ['dissecting_denial']
---

The default location where you can find this logging depends a bit on the distribution, but
generally it is either in `/var/log/avc.log` if you are not running the Linux audit daemon, and in
`/var/log/audit/audit.log` or `/var/log/audit.log` if you are. This logging is very verbose, mainly
because you need many details in order to troubleshoot problems.

But before we take a look at the denials, we also want to give you a heads up.

1. Not every denial you find in the logs is a problem by itself. Some denials are cosmetic, meaning
that they do occur but do not influence the behavior of an application. This is often because of an application development malpractice (like not properly closing file descriptors) or because of high-level library functions where only a small fraction of the features are used by an application.

2. Denials are logged as they come along. That means that you will see a lot of denials, and
although many will be related to each other (one denial leads to the other) many will also have
nothing to do with the problem you are investigating.

3. If there are too many denials succeeding each other, they might be suppressed by the Linux
kernel; if that happens, you will get a message like the following, so if you find this message in
your logs you have to understand that you are not seeing everything that SELinux might be reporting:

```
Mar 12 17:46:42 hpl kernel: [   14.453644] audit_printk_skb: 84 callbacks suppressed
```

So let's take a look at one denial. This one comes from the audit log (which you can tell from the start of the log, type=AVC, which you will not see in the avc.log as it is implied there).

```
type=AVC msg=audit(1363289005.532:184): avc:  denied  { read } for
pid=29199 comm="Trace" name="online" dev="sysfs" ino=30
scontext=staff_u:staff_r:googletalk_plugin_t
tcontext=system_u:object_r:sysfs_t tclass=file
```

We warned you that it was verbose ;-)
