---
number: 11
title: Multi Category Security
description: Explore the more advanced mode of SELinux
attribution_url: https://selinuxproject.org/page/MultiCategorySecurity
---

Multi-Category Security (MCS) is an optional addition in SELinux that allows users to add categories
to processes and files. This adds the additional constraint to the access check requiring that the
categories that the process has must be a superset of the categories of the files it is accessing.
The number of categories supported by the system is configured by policy; Fedora supports 1024, c0,
c1,... c1022, c1023. For example, if a process has categories c1,c3, it can access files that have
category c1, files that have category category c3, files that have categories c1 and c3, and files
that have no categories. It will not be able to access a file that has category c4, or a file that
has categories c3 and c6.

Categories can optionally be translated (mapped) into more descriptive names, such as Engineering,
Marketing, Payroll, and CompanyNDA. A file may have multiple categories. For example, if there was a
technical report but it was under a non-disclosure agreement (NDA), the file might have the
categories Engineering,CompanyNDA. The category names can be configured in the
_/etc/selinux/NAME/setrans.conf_ file.

```
s0:c0=Engineering
s0:c1=Marketing
s0:c2=Payroll
s0:c3=CompanyNDA
s0:c0,c3=Engineering_NDA
```

The s0 portion is required, as MCS is implemented using SELinux's Multi-Level Security (MLS)
support.

The categories on a file can be changed by using the `chcat` command. For example, to add the
CompanyNDA to a file:

```
chcat +CompanyNDA myfile.doc
```

Similarly, to remove the Engineering category:

```
chcat -- -Engineering myfile.doc
```

The `--` is required to specify that the categories being removed are not options for `chcat`. To
completely set the category set (replacing the existing categories):

```
chcat Marketing,CompanyNDA myfile.doc
```

Now that the file has the correct categories, programs should be run with categories.

```
runcon -l Engineering evolution
```

This will run the evolution email program with the Engineering category. Now this instance of
evolution will be able to attach files with either no categories or the Engineering category. It
will be prevented from accidentally attaching CompanyNDA files, since evolution has the Engineering
category, which is not a superset of the CompanyNDA category.
