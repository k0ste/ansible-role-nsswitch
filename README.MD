ansible-nsswitch
==================

The Name Service Switch (NSS) configuration file, `/etc/nsswitch.conf`, is used by
the GNU C Library and certain other applications to determine the sources from
which to obtain name-service information in a range of categories, and in what
order. Each category of information is identified by a database name.

Ansible versions
-----------------

Ansible 2.0 is required.

Extra
------

database source is not validated and pass as-is. For all possible sources please
consult `nsswitch.conf(5)`.

Example configuration
-------------------------

```yaml
---
# The following databases are understood by the GNU C Library
nsswitch:
# aliases - Mail aliases, used by getaliasent(3) and related functions.
  aliases: ''
# ethers - ethernet numbers.
  ethers:
  - 'files'
  - 'ldap'
# group - groups of users, used by getgrent(3) and related functions.
  group:
  - 'compat'
  - 'mymachines'
  - 'systemd'
  - 'ldap'
# hosts - host names and numbers, used by gethostbyname(3) and related functions.
  hosts:
  - 'files'
  - 'mymachines'
  - 'resolve'
  - '[!UNAVAIL=return]'
  - 'dns'
  - 'myhostname'
# initgroups - supplementary group access list, used by getgrouplist(3) function.
  initgroups: ''
# netgroup - network-wide list of hosts and users, used for access rules.
# C libraries before glibc 2.1 supported netgroups only over NIS.
  netgroup:
  - 'ldap'
  - 'files'
# networks - network names and numbers, used by getnetent(3) and related functions.
  networks:
  - 'files'
  - 'ldap'
# passwd - User passwords, used by getpwent(3) and related functions.
  passwd:
  - 'compat'
  - 'mymachines'
  - 'systemd'
  - 'ldap'
# protocols - Network protocols, used by getprotoent(3) and related functions.
  protocols:
  - 'files'
  - 'ldap'
# publickey - Public and secret keys for Secure_RPC used by NFS and NIS+.
  publickey:
  - 'files'
# rpc - Remote procedure call names and numbers, used by getrpcbyname(3) and
# related functions.
  rpc:
  - 'files'
  - 'ldap'
# services - Network services, used by getservent(3) and related functions.
  services:
  - 'files'
  - 'ldap'
# shadow - Shadow user passwords, used by getspnam(3) and related functions.
  shadow:
  - 'compat'
  - 'ldap'
# The GNU C Library ignores databases with unknown names. Some applications use
# this to implement special handling for their own databases. For example, sudo
# consults the sudoers database.
  sudoers:
  - 'ldap'
  - 'files'
```
