---
number: 6
title: Dissecting an SELinux Denial
description: Learn how to interpret and understand SELinux denials
attribution_url: https://wiki.gentoo.org/wiki/SELinux/Tutorials/Where_to_find_SELinux_permission_denial_details
next_tutorials: ['audit2allow']
---

Here is a SELinux denial example:

```
type=AVC msg=audit(1363289005.532:184): avc:  denied  { read } for
pid=29199 comm="Trace" name="online" dev="sysfs" ino=30
scontext=staff_u:staff_r:googletalk_plugin_t
tcontext=system_u:object_r:sysfs_t tclass=file
```

Once you get to know this denial structure, you can translate this into the following:

```
The Trace process with PID 29199 tried to read a file called online
on a file system hosted on the sysfs device. This file has inode
number 30, and has the security context system_u:object_r:sysfs_t
assigned to it. The Trace process itself is running with the
staff_u:staff_r:googletalk_plugin_t context (domain).
```

The following section gives a part by part explanation. We do want to tell you though that the logs
can be a bit different based on what is denied - for instance, a file read access shows a few
different parts than a socket connect denial. The majority of fields however will be present in all
cases.

### Log type
Log Part: `type=AVC`

Only in the _audit.log_ file; it informs the user what kind of audit log type this is. So in our
case, it is an AVC log entry.

### Timestamp
Log Part: `msg=audit(1363289005.532:184)`

Timestamp in seconds since epoch, meaning the number of seconds since January 1st, 1970. You can
convert this to a more human readable format using `date -d @` followed by the number, like so:

```
user $date -d @1363292159.532

Thu Mar 14 21:15:59 CET 2013
```

### Log type (again)
Log Part: `avc:`

Informs the user what kind of log entry this is. In this case, an AVC log entry.

### State (if enforced)
Log Part: `denied`

What SELinux did, which can be either _denied_ or _granted_. Note that, if SELinux is in permissive
mode, then it will still log as _denied_ even though it was allowed.

### Permission
Log Part: `{ read }`

The permission that was requested / executed. In this case, it is a read operation. Sometimes the
permission contains a set (like _{ read write }_ but in most cases, it is a single permission
request).

### Process PID
Log Part: `for pid=29199`

The process identifier of the process that took the action (in this case, tried to read)

### Process CMD
Log Part: `comm="Trace"`

The process command (without arguments, and limited to 15 characters), which helps users identify
what the process was in case the process is already gone (a PID is only useful if the process is
still running).

### Target name
Log Part: `name="online"`

The name of the target (in this case, the file name). This field depends heavily on the target
itself; it can also be _path=_, _capability=_, _src=_ and more. But in those cases, its purposes
should be clear from the rest of the log.

### Device
Log Part: `dev="sysfs"`

Device on which the target resides (in case of a file or file system). In this case, the device is
_sysfs_ so we have the hint immediately that this is for something inside _/sys_. Other valid
examples are _dev=md-0_, _dev=sda1_ or _dev=tmpfs_.

### Inode Number
Log Part: `ino=30`

The inode number of the target file. In this case, since we know it is on the _sysfs_ file system
(and thus in _/sys_), we can look for this file using _find_:

```
user $find /sys -xdev -inum 30

/sys/devices/system/cpu/online
```

### Source Context
Log Part: `scontext=staff_u:staff_r:googletalk_plugin_t`

The security context of the process (the domain).

### Target Context
Log Part: `tcontext=system_u:object_r:sysfs_t `

The security context of the target resource (in this case the file).

### Target Class
Log Part: `tclass=file`

The class of the target. We have seen _file_ already, and _dir_ shouldn't surprise you either.
SELinux supports a whole lot of classes.
