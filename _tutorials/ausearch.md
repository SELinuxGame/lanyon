---
number: 8
title: Searching for Denials with ausearch
description: Learn how to search for previous denials with the `ausearch` tool
attribution_url: https://wiki.gentoo.org/wiki/SELinux/Tutorials/Where_to_find_SELinux_permission_denial_details
next_tutorials: ['audit2allow']
---

The friendly developers that work with SELinux on a daily basis have made a few tools that help you
identify SELinux-related issues.

The `ausearch` utility is no SELinux-specific utility. It is a Linux audit related utility, which
parses the audit logs and allows you to query the entries in the logs. One of the advantages that it
shows is that it already converts the time stamp into a human readable one.

```
root #ausearch -m avc --start recent
time->Thu Mar 14 21:15:57 2013
type=AVC msg=audit(1363292157.560:188): avc:  denied  { read } for  pid=29495 comm="Trace"
name="online" dev="sysfs" ino=30 scontext=staff_u:staff_r:googletalk_plugin_t
tcontext=system_u:object_r:sysfs_t tclass=file
```

The _recent_ start gives the denials from the last 10 minutes. You can also use today for, well,
today's denials.

<p style="padding-top:30px">
  <h2>Tools</h2>
</p>

[`ausearch`](https://linux.die.net/man/8/ausearch) searches logs for errors and can be useful for
showing SELinux denials
