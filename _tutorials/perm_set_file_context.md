---
number: 7
title: Permanently Set a File Context
description: Learn how to set file context by modifying the policy.
attribution_url: https://selinuxproject.org/page/FileLabelRecipe
next_tutorials: ['audit2allow']
---

The `chcon` program can change the context of a file; however, changes made
with `chcon` are not preserved if the file is relabeled with `restorecon`, or
if the entire file system is relabeled using `touch /.autorelabel` and then
rebooted. The `semanage` program can make persistent customizations to the
SELinux policy configuration.

To run `semanage`, you must be the Linux root user and in a role allowed to
run `semanage`, such as _sysadm_r_ or _unconfined_r_. The following example
uses `semanage` to set the _myfile_t_ type for the "/path/to/myfile" file:

```
# semanage fcontext -a -t myfile_t /path/to/myfile
```

This `semanage` command adds an entry in the system file contexts. This entry
will be persistent, even after the distribution policy is updated. If you
change policies, for example, from targeted to MLS, you must re-run the above
command to add the entry to the new policy. Run the restorecon command to
apply the changes added via `semanage fcontext`:

```
# restorecon /path/to/myfile
# ls -Z /path/to/myfile
system_u:object_r:myfile_t /path/to/myfile
```

<p style="padding-top:30px">
  <h2>Tools</h2>
</p>

* [`semanage`](https://linux.die.net/man/8/semanage) allows for policy
management. Specifically the `semanage fcontext` can alter the default file
contexts in the policy for any given file or folder.

* [`restorecon`](https://linux.die.net/man/8/restorecon) restores the default
SELinux file context for a file or folder.

* [`chcon`](https://linux.die.net/man/1/chcon) changes the file SELinux
security context.
