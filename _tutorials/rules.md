---
number: 4
title: SELinux Rules and Modules
description: Learn the basics of how SELinux determines if an action is allowed or not.
attribution_url: https://selinuxproject.org/page/BasicConcepts
next_tutorials: ['modules']
---

The primary security mechanism of SELinux is type enforcement, meaning that
rules are specified using the type of the process and object:

```
allow user_t user_home_t:file { create read write unlink };
```

This rule states that the _user_t_ type is allowed to create, read, write,
and delete files with the user_home_t type.

<p style="padding-top:30px">
  <h2>Policies</h2>
</p>

A groups of rules together make a module, which collectively allow all of the
necessary permissions a given application needs. List all of the installed
policies with the `semodule -l` command.

<p style="padding-top:30px">
  <h2>Tools</h2>
</p>

[`semodule`](https://linux.die.net/man/8/semodule) can list the installed
policies with the `selinux -l` command.
