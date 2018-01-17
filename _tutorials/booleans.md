---
number: 6
title: Booleans
description: Learn how to set and check for SELinux booleans
attribution_url: https://wiki.centos.org/TipsAndTricks/SelinuxBooleans
next_tutorials: ['audit2allow']
---

SELinux uses booleans to makes its policy more flexible. Typically a basic policy is pretty strict,
but it can be made more permissive with booleans. For example, the SELinux policy that ships with
ftpd prevents reading from nfs. That behavior can be changed with the `allow_ftpd_use_nfs` boolean.

List all of the booleans on your system with `getsebool` as follows:

```
getsebool -a
```

Set a boolean value with `setsebool`:

```
setsebool -P allow_ftpd_use_nfs=1
```

If the `-P` flag is used, the boolean change will be permanent.

<p style="padding-top:30px">
  <h2>Tools</h2>
</p>

[`getsebool`](https://linux.die.net/man/8/getsebool) shows SELinux boolean values.

[`setsebool`](https://linux.die.net/man/8/setsebool) sets the current state of a particular SELinux
boolean or a list of booleans to a given value.
