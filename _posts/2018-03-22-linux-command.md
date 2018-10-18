---
layout: default
title: linux command
---

# Linux command

## 查看 Linux 发型版本信息

```shell
[root@AppBox-AP ~]# cat /proc/version
Linux version 2.6.39-400.17.1.el6uek.x86_64 (mockbuild@ca-build44.us.oracle.com) (gcc version 4.4.7 20120313 (Red Hat 4.4.7-3) (GCC) ) #1 SMP Fri Feb 22 18:16:18 PST 2013
[root@AppBox-AP ~]# lsb_release -a
LSB Version:	:base-4.0-amd64:base-4.0-noarch:core-4.0-amd64:core-4.0-noarch:graphics-4.0-amd64:graphics-4.0-noarch:printing-4.0-amd64:printing-4.0-noarch
Distributor ID:	OracleServer
Description:	Oracle Linux Server release 6.4
Release:	6.4
Codename:	n/a
```

## 查看 Linux 内核版本信息

```shell
uname -a
```
