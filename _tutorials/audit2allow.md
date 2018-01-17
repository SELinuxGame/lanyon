---
number: 8
title: Fixing AVC denials
description: Learn how to use audit2allow to write a "workaround" SELinuxpolicy
attribution_url: https://selinuxproject.org/page/Audit2allowRecipe
---

If SELinux is denying access for something you believe should be allowed, you
can add rules to your policy with the `audit2allow` program.

First, run the `ps -ef | grep auditd` command to find out if `auditd` is
running:

```
# ps -ef | grep auditd
root        69     2  0 Sep26 ?        00:00:00 [kauditd]
root      1159     1  0 Sep26 ?        00:00:00 auditd
```

If `auditd` is running, as shown above, use the `-a` option with
`audit2allow`. If it is not running, use the `-d` option.

The `-l` option reads denials since the last policy reload, and the `-M`
option creates a module with rules to allow those denials.

Do not use the `-M` option to specify the same module name more than once.
For example, if you run the command below once with `-M local`, and want to
run it again later, choose a different name, such as `-M local2`.

```
# audit2allow -l -a -M local
******************** IMPORTANT ***********************
To make this policy package active, execute:

semodule -i local.pp
```

You can view the rules to be added in the _local.te_ file. If you are
satisfied, run the `semodule -i local.pp` command to install the module. You
can mail an SELinux list, such as the Fedora SELinux list or the NSA SELinux
mailing list, to ask for review of your module before you install it. 

<p style="padding-top:30px">
  <h2>Tools</h2>
</p>

* [`audit2allow`](https://linux.die.net/man/1/audit2allow) Generate a SELinux
policy from logs of denied operations.
